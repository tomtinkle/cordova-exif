# Cordova Exif with XMP

This plugin, is the simplest way to get exif data and xmp data of images at Cordova platform (Phonegap)

## Getting Started

### Installing

	cordova plugin add https://github.com/tomtinkle/cordova-exif.git --save

### Usage

Pass imageURI and get the object with EXIF and XMP information

```javascript
CordovaExif.readData(imageURI, function(resultObject) {
  // get exif data
  console.log(resultObject.exif);
  // get xmp data (array)
  var xmparr = resultObject.xmp;
  for (var i = 0; i &lt; xmparr.length; i++) {
    console.log(xmparr[i].origin); // xmp origin data
    console.log(xmparr[i].xml);    // convert xml data
    console.log(xmparr[i].dom);    // parse dom data
  }
});
```

OBS: To get the Exif data, you application need to have access permission to the file.
If you are using Cordova version 3.3 or later, install the following plugins:
```sheel
cordova plugin add org.apache.cordova.camera
cordova plugin add org.apache.cordova.file
```

## What is Exif?

Is a standard followed by manufacturers of digital cameras that record information about the technical conditions of image capture on the image file itself in the form of tagged metadata.

If you want know more about technical information, see these links:
- [Exif Standard 2.2](http://www.kodak.com/global/plugins/acrobat/en/service/digCam/exifStandard2.pdf)
- [Description of Exif file format](http://www.media.mit.edu/pia/Research/deepview/exif.html)
- [Exif Tags](http://www.sno.phy.queensu.ca/~phil/exiftool/TagNames/EXIF.html)

## Example of Exif Data on photo

| Key | Value |
|-----|-------|
| Make | Canon |
| Model | Canon EOS 60D |
| DateTime | 2014:02:16 15:00:00 |
| XResolution | 240 |
| YResolution | 240 |
| Resolution Unit | Inch |
| FNumber | f/8.0 |
| Focal Length | 100 mm |
| GPS Latitude | -8.053889 |
| GPS Longitude | -34.880833 |
| Exposure Program | Aperture priority |
| Flash | Flash fired, compulsory flash mode |
| Metering Mode | Pattern |
| Exposure Time | 0.004 |
| Shutter SpeedValue | 7.965784 |
| Custom Rendered  | Normal process |
| White Balance | Auto white balance |
| ISO Speed Ratings | (100) |
| Lens Model | EF100mm f/2.8L Macro IS USM |
| Lens Serial Number | 0000023967 |
| Lens Specification | (100,100,0,0) |
| This is just somes examples, has much more informations. | ... |


## What is XMP?
The Extensible Metadata Platform (XMP) is an ISO standard, originally created by Adobe Systems Inc., for the creation, processing and interchange of standardized and custom metadata for digital documents and data sets.

XMP standardizes a data model, a serialization format and core properties for the definition and processing of extensible metadata. It also provides guidelines for embedding XMP information into popular image, video and document file formats, such as JPEG and PDF, without breaking their readability by applications that do not support XMP. Therefore, the non-XMP metadata have to be reconciled with the XMP properties. Although metadata can alternatively be stored in a sidecar file, embedding metadata avoids problems that occur when metadata is stored separately.

This was quoted from [wikipedia](https://en.wikipedia.org/wiki/Extensible_Metadata_Platform).



## Complete Example

This example show how its simple get exif information of photo taken by a smartphone.

```javascript
var options = {
	quality: 90,
	sourceType: 2,
	destinationType: 1,
};

function onSuccess(imageURI) {
	CordovaExif.readData(imageURI, function(resultObject) {
		// get exif data
		console.log(resultObject.exif);
		// get xmp data (array)
		var xmparr = resultObject.xmp;
		for (var i = 0; i &lt; xmparr.length; i++) {
			console.log(xmparr[i].origin); // xmp origin data
			console.log(xmparr[i].xml);    // convert xml data
			console.log(xmparr[i].dom);    // parse dom data
		}
	});
};

function onFail(message) {
	console.log('Failed because: ' + message);
};

navigator.camera.getPicture(onSuccess, onFail, options);
```

## About

#### License?
Cordova Exif is released under the terms of the [MIT license](https://github.com/tomtinkle/cordova-exif/blob/master/MIT-LICENSE).
