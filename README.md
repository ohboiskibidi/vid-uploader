# vid-uploader
idk what to put herte
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Upload Video</title>
</head>
<body>
  <h1>Upload a Video</h1>
  <form id="uploadForm" enctype="multipart/form-data" method="POST" action="/api/upload">
    <input type="file" name="video" accept="video/*" required />
    <button type="submit">Upload</button>
  </form>
</body>
</html>
import fs from 'fs';
import path from 'path';
import formidable from 'formidable';

export const config = {
  api: {
    bodyParser: false,
  },
};

export default function handler(req, res) {
  if (req.method === 'POST') {
    const form = new formidable.IncomingForm({ uploadDir: '/tmp', keepExtensions: true });

    form.parse(req, (err, fields, files) => {
      if (err) {
        console.error(err);
        return res.status(500).send('Error uploading file.');
      }

      const file = files.video;
      if (!file) {
        return res.status(400).send('No file uploaded.');
      }

      res.status(200).send('✅ Video uploaded successfully!');
    });
  } else {
    res.status(405).send('Method Not Allowed');
  }
}
{
  "cleanUrls": true,
  "rewrites": [
    { "source": "/upload", "destination": "/api/upload" }
  ]
}
{
  "type": "module",
  "dependencies": {
    "formidable": "^3.5.0"
  }
}
https://video-uploader-yourname.vercel.app
