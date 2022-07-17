<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>'Hello, world!' example</title>
</head>
<body>

<h1>'Hello, world!' example</h1>

<div id="example1"></div>

<script src="./assets/js/pdfobject.min.js"></script>
<script>PDFObject.embed("./assets/pdf/cv_yujin.pdf", "#example1");</script>

<style>
.pdfobject-container { height: 70rem; border: 20rem solid rgba(0,0,0,.1); }
</style>
</body>
</html>
