---
date: 2024-05-12 22:37:01
title: "Call"
categories:
  - events
  - 2034
---

## Call for Papers

Please submit your papers for consideration.

<div id="videoContainer">
    <input type="file" id="fileInput" accept="video/*" style="display: none;">
    <button id="selectFileButton" style="padding: 10px 20px; margin: 10px; background-color: #4CAF50; color: white; border: none; border-radius: 5px; cursor: pointer;">Select Video</button>
    <div id="progressContainer" style="display: none; margin: 10px;">
        <div id="progressBar" style="width: 100%; background-color: #f3f3f3; border-radius: 5px;">
            <div id="progressFill" style="width: 0%; height: 20px; background-color: #4CAF50; border-radius: 5px; text-align: center; color: white;"></div>
        </div>
        <span id="progressText">0%</span>
    </div>
    <button id="uploadButton" style="display: none; padding: 10px 20px; margin: 10px; background-color: #2196F3; color: white; border: none; border-radius: 5px; cursor: pointer;">Upload Video</button>
</div>

<script>
document.addEventListener("DOMContentLoaded", function() {
    var fileInput = document.getElementById('fileInput');
    var selectFileButton = document.getElementById('selectFileButton');
    var uploadButton = document.getElementById('uploadButton');
    var progressContainer = document.getElementById('progressContainer');
    var progressFill = document.getElementById('progressFill');
    var progressText = document.getElementById('progressText');
    var selectedFile;

    selectFileButton.addEventListener('click', function() {
        fileInput.click();
    });

    fileInput.addEventListener('change', function(event) {
        selectedFile = event.target.files[0];
        if (selectedFile) {
            uploadButton.style.display = 'inline-block';
        }
    });

    uploadButton.addEventListener('click', function() {
        if (!selectedFile) return;

        var fileName = 'video_' + Date.now() + '_' + generateRandomString(8) + '.mp4';
        var formData = new FormData();
        formData.append('file', selectedFile, fileName);

        var xhr = new XMLHttpRequest();
        xhr.open('POST', '/video/', true);

        xhr.upload.onprogress = function(event) {
            if (event.lengthComputable) {
                var percentComplete = Math.round((event.loaded / event.total) * 100);
                progressFill.style.width = percentComplete + '%';
                progressText.textContent = percentComplete + '%';
            }
        };

        xhr.onloadstart = function() {
            progressContainer.style.display = 'block';
            progressFill.style.width = '0%';
            progressText.textContent = '0%';
        };

        xhr.onload = function() {
            if (xhr.status === 200) {
                var videoUrl = '/video/' + fileName;
                var videoElement = document.createElement('video');
                videoElement.src = videoUrl;
                videoElement.controls = true;
                videoElement.style.maxWidth = '100%';
                videoElement.style.marginTop = '10px';
                videoContainer.appendChild(videoElement);
                alert('Upload complete!');
            } else {
                console.error('Failed to upload video. Status:', xhr.status);
                alert('Failed to upload video. Please try again.');
            }
        };

        xhr.onerror = function() {
            console.error('Failed to upload video. Network error.');
            alert('Failed to upload video due to a network error. Please try again.');
        };

        xhr.send(formData);
    });
});

function generateRandomString(length) {
    var result = '';
    var characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
    for (var i = 0; i < length; i++) {
        result += characters.charAt(Math.floor(Math.random() * characters.length));
    }
    return result;
}
</script>
