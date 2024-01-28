# Media College

```
Author      : Media College
Department  : WEB 
Year        : 2024 
Description : Portfoile API
Doc         : postman
```

# Indledning.

Opsæt følgende `endpoints` i en ny **Portfolios Api** collection.

Opret følgende mapper i din `Portfolios Api` collection.

Mapper:

:file_folder: Authors   
:file_folder: Author   
:file_folder: Galleries     
:file_folder: Images

Opret følgende request under tilhørende mappe.




:file_folder: Authors   

```javascript
Get Authors
http://localhost:3000/api/authors
```
```javascript
Get Authors By Gallery
http://localhost:3000/api/author?gallery=[gallery]
```

:file_folder: Author  

```javascript
Get Author By Id
http://localhost:3000/api/author?id=[authorId]
```

```javascript
Get Author By Name
http://localhost:3000/api/author?name=[authorName]
```

```javascript
Get Author By Url Name
http://localhost:3000/api/author?urlname=[urlname]
```

```javascript
Get Author By Folder
http://localhost:3000/api/author?folder=[folder]
```




:file_folder: Galleries 





```javascript
Get Galleries
http://localhost:3000/api/galleries
```

```javascript
Get Gallery By ID
http://localhost:3000/api/gallery?id=[galleryId]
```

```javascript
Get Gallery By Name
http://localhost:3000/api/gallery?name=[galleryName]
```




:file_folder: Images 





```javascript
Get Images
http://localhost:3000/api/images
```

```javascript
Get Images By Author
http://localhost:3000/api/images?author=[author]
```

```javascript
Get By Galleryname
http://localhost:3000/api/images?gallery=[galleryName]
```

```javascript
Get By Page
http://localhost:3000/api/images?page=[pagenumber]
```

```javascript
Get By Searchterm
http://localhost:3000/api/images?searchterm=[term]
```


