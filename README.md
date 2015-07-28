# HTML FileAPI Demos
Below are a few demos for HTML5's File API. *Note: these demos may not work in all browsers.*

## Read File Meta Information
You can read meta information with most browsers by simply accessing the File object provided by the `input[type=file]` element. In the below example, the input[type=file] has an ID of **singleFileInfo**.

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

## Read File Contents
Here's where the **FileAPI** really starts to bloom. Here, we can read the file contents BEFORE ever even hitting a server. In this example, we are reading a CSV, complete with headers, and outputting the contents into a table. Here, the `input[type=file]` has an ID of **singleFileContents**. There's also a `thead > tr` with an ID of **contentsHeader** and a `tbody` with an ID of **contentsBody**. Here, we will break up the file first by new lines and then by commas. This demo will work with your typical CSV where the values of the cells do **NOT** have a comma in them. Providing additional support for this will just require tinkering with the `.split` statements.

```javascript
var fileInput = document.getElementById('singleFileContents'),
	contentsHeader = document.getElementById('contentsHeader'),
	contentsBody = document.getElementById('contentsBody');
fileInput.addEventListener('change', displayFileContents);

function displayFileContents() {
	var reader = new FileReader();
	reader.readAsText(fileInput.files[0]);

	// Clear all the things
	contentsHeader.innerHTML = '';
	contentsBody.innerHTML = '';

	reader.onload = function(e) {
		var contents = reader.result,
			lines = contents.split('\n'),
			headers = lines.shift().split(',');

		headers.forEach(function(header) {
			var th = document.createElement('th');
			th.appendChild(document.createTextNode(header));
			contentsHeader.appendChild(th);
		});

		lines.forEach(function(line) {
			var values = line.split(','),
				tr = document.createElement('tr');
			values.forEach(function(value) {
				var td = document.createElement('td');
				td.appendChild(document.createTextNode(value));
				tr.appendChild(td);
			});
			contentsBody.appendChild(tr);
		});
	}
}
```


## Preview Image
This example is really useful when wanting to preview an image before actually uploading. This demo will take a selected image and create a base64 URL for the selected image and then change the src of an `image` element. In this demo, we have an `input[type=file]` element with an ID of **singleFileThumbnail** as well as an `img` element with an ID of `fileThumbnail`.

```javascript
var fileInput = document.getElementById('singleFileThumbnail');
fileInput.addEventListener('change', displayFileContents);

function displayFileContents() {
	var reader = new FileReader();
	reader.readAsDataURL(fileInput.files[0]);

	reader.onload = function(e) {
		document.getElementById('fileThumbnail').src = reader.result;
	}
}
```