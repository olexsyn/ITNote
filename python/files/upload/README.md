# Загрузка файлов пользователя на сервер

**HTML** _some.htm_

```html
<html>
<body>
	<form enctype="multipart/form-data" action = "upl.py" method = "post">
	<p>File: <input type="file" name="uplfile" /></p>
	<p><input type="submit" value="Upload" /></p>
</form>
</body>
</html>
```

**CGI**  _upl.py_

```python
#!/usr/bin/python

import cgi, os.path

UPLOAD_DIR = '/var/www/site/upload'

form = cgi.FieldStorage()

if "uplfile" in form:
	upl_file = form['uplfile']  # upl_file is now an object
	if upl_file.filename:

		uploaded_file_path = os.path.join(UPLOAD_DIR, os.path.basename(upl_file.filename))
		with open(uploaded_file_path, 'wb') as fout:
			while True:
				chunk = upl_file.file.read(100000)
				if not chunk:
					break
				fout.write(chunk)

		# # load the written file to display it
		# with open(uploaded_file_path, 'r') as fin:
		# 	inFileData = ""
		# 	for line in fin:
		# 		inFileData += line

	message = 'The file ' + upl_file.filename + ' was uploaded successfully'
else:
	message = 'No file was uploaded'

print('Content-Type: text/html\n')
print(f'{message}')
```
