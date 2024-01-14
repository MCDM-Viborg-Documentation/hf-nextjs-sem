# Rettelse til jeres /lib/data.service.js

:bulb:  Efter første gennemgang af løsninger er der en rettelse til selve projektet.

Erstat **ALT** indhold i filen med dette:

*Skulle i selv have oprettet funktioner skal i selvfølgelig gemme den dem. ALT andet skal udskiftes.*


```javascript

import dbConnect from "./db/dbConnect.mjs";
import authorModel from "./db/models/author.model.mjs";
import galleryModel from "./db/models/gallery.model.mjs";
import imageModel from "./db/models/image.model.mjs";

/*

    Get all galleries

*/
export const fetchGalleries = async () => {
    
    console.log('fetchGalleries')

    try {

        await dbConnect();

        let result = await galleryModel.find({});

        return JSON.parse(JSON.stringify(result))

    } catch (error) {

        console.log(error)

    }


};

/*

    Get gallery by name

*/
export const fetchGalleryById = async (name) => {

    console.log('fetchGalleryById', name)

    try {

        await dbConnect();
        let result = await galleryModel.find({name: name});

        return JSON.parse(JSON.stringify(result[0]))

    } catch (error) {

        console.log(error)

    }
};

/*

    Get Gallery for Author by gallery name

*/
export const fetchAuthorsByGalleryName = async (name) => {

    console.log('fetchAuthorsByGalleryName', name)
    try {

        await dbConnect();
        let result = await authorModel.find({gallery: name});
    
        return JSON.parse(JSON.stringify(result))

    } catch (error) {

        console.log(error)

    }


};

/*

    Get Author by name

*/
export const fetchAuthorByNicUrl = async (niceUrl) => {

    console.log('fetchAuthorByNicUrl', niceUrl)
    try {

        await dbConnect();
        let result = await authorModel.find({niceUrl: niceUrl});
    
        return JSON.parse(JSON.stringify(result[0]))

    } catch (error) {

        console.log(error)

    }

};

/*

    Get Authors

*/
export const fetchAuthors = async () => {

    console.log('fetchAuthors')
    try {

        await dbConnect();
        let result = await authorModel.find({});
    
        return JSON.parse(JSON.stringify(result))

    } catch (error) {

        console.log(error)

    }

};

/*

    Get Images for author by author name

*/
export const fetchImagesForAuthor = async (author) => {

    console.log('fetchImagesForAuthor', author)

    try {

        await dbConnect();
        let result = await imageModel.find({"author" : { $regex:author, $options: 'i' } });
    
        return JSON.parse(JSON.stringify(result))

    } catch (error) {

        console.log(error)

    }

};

/*

    Get all images for gallery

*/
export const fetchImagesForGallery = async (name) => {

    console.log('fetchImagesForGallery', name)

    try {

        await dbConnect();
        let result = await imageModel.find({"gallery" :  { $regex:name, $options: 'i' } });
    
        return JSON.parse(JSON.stringify(result))

    } catch (error) {

        console.log(error)

    }

};
```