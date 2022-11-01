# C-Sharp-Live-Project
## Introduction
At the end of the C# course at The Tech Academy, I worked alongside other students creating an MVC app using Entity Framework. The project was meant to imitate a real work environment and was run following Agile and SCRUM principles with a sprint planning session, daily stand up meetings, and retrospectives at the end of both weeks of the two week sprint. Below is a description of the functionality with code snippets of what I created.

## Acquired Skills
- Agile/Scrum
- Programming in a team environment
- Azure DevOps
- Working in an existing codebase and adding features
- Working with a remote repository with git

## CRUD Functionality
The project we worked on as a team was a website for a Portland theater group, my job was to create the portion of the site that would allow members of the theater group to easily upload and modify entries for production photos.
#### I created a model and used Entity Framework to generate an associated SQL table and scaffold the basic CRUD pages:
```
public class ProductionPhoto
    {
        public int ProductionPhotoId { get; set; }
        public byte[] PhotoFile { get; set; }
        public string Title { get; set; }
        public string Description { get; set; }
    }
```

#### I then had to create a method to convert uploaded images into a byte array to allow them to be stored in the SQL database:
```
public byte[] imageToByteArray(HttpPostedFileBase photoUpload)
        {
            byte[] bytes;
            using (BinaryReader br = new BinaryReader(photoUpload.InputStream))
            {
                bytes = br.ReadBytes(photoUpload.ContentLength);
            }
            return bytes;
        }
```

#### And convert the byte array back into an image using razor syntax when it needed to be displayed:
```
<img src="data:image/jpg;base64,@Convert.ToBase64String(item.PhotoFile)" />
```
