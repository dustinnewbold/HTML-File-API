# HTML-File-API
A demo for HTML5's File API

## Read File Meta Information
You can read meta information with most browsers by simply accessing the File object provided by the input[type=file] element. In the below example, the input[type=file] has an ID of *singleFileInfo*

```javascript
var fileInput = document.getElementById('singleFileInfo');
fileInput.addEventListener('change', displayFileInformation);

function displayFileInformation() {
	document.getElementById('singleFileName').innerHTML = fileInput.files[0].name;
	document.getElementById('singleFileType').innerHTML = fileInput.files[0].type;
	document.getElementById('singleFileSize').innerHTML = Math.round((fileInput.files[0].size * 10) / 1024) / 10 + ' Kb';
	document.getElementById('singleFileModified').innerHTML = fileInput.files[0].lastModifiedDate;
	text = fileInput.files[0].lastModifiedDate;
}
````