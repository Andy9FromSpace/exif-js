# Exif.js (Google Apps Script compatible version)

A JavaScript library for reading [EXIF meta data](https://en.wikipedia.org/wiki/Exchangeable_image_file_format) from image files.

This version has been modified to make it compatible with Google Apps Script.

It can be used to get extended image metadata like IPTC and XMP over the Google Apps Script API, since the Google Drive API only provides basic EXIF metadata.
For that you have to enable Google Drive API access in your Google Apps Script project (https://developers.google.com/apps-script/reference/drive/).

**Note**: The EXIF standard applies only to `.jpg` and `.tiff` images. EXIF logic in this package is based on the EXIF standard v2.2 ([JEITA CP-3451, included in this repo](/spec/Exif2-2.pdf)).

## Install
Add exif.js to your Google Apps Script project.

## Usage
Exif.js adds a global `EXIF` variable.

**JavaScript**:
```javascript
function loadJpegMetadataFromDriveFileId(driveFileId) {
  var driveFile = DriveApp.getFileById(driveFileId);  
  var blob = driveFile.getBlob();
  var bytes = blob.getBytes();
  var file = new File(bytes);
  EXIF.enableXmp();
  var metadata = EXIF.readFromBinaryFile(file);
  return metadata;
}

function loadJpegMetadataFromBase64String(imageBase64String) {
  var bytes = Utilities.base64Decode(imageBase64String);
  var file = new File(bytes);
  EXIF.enableXmp();
  var metadata = EXIF.readFromBinaryFile(file);
  return metadata;
}
```

**XMP**
Since issue #53 was merged also extracting of XMP data is supported. To not slow down this is optional, and you need to call `EXIF.enableXmp();` before using `..getDatat()`.

## Contributions
This is an [open source project](LICENSE.md). Please contribute by forking this repo and issueing a pull request. The project has had notable contributions already, like reading ITPC data.

You can also contribute by [filing bugs or new features please issue](/exif-js/issues).
Or improve the documentation. Please update this README when you do a pull request of proposed changes in base functionality.
