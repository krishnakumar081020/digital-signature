# digital-signature//HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Upload your document</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <link rel="stylesheet" href="halleyx.css">
    
    
</head>
<body>
  <div class="drag-area">
    
    <header>Drag and Drop your file</header>
    <span>or</span>
    <button>Upload</button>
    <input type="file" hidden>
  </div>
<script src="haleyx.js"></script> 
<h4> This file should be accept only one pdf document and its size should not exceed 12MB</h4>
</body>
<link rel="script" type="script" href="haleyx.script">
</html>
# digital-signature//css

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;

}

body{
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 70vh;
  background: white;
}

.drag-area{
  border: 2px dashed black;
  height: 300px;
  width: 400px;
  border-radius: 5px;
  display: flex;
  align-items: center ;
  justify-content: center;
  flex-direction: column;
}
.drag-area.active{
  border: 2px solid black;
}

.drag-area header{
  font-size: 30px;
  font-weight: 500;
  color: black;
}
.drag-area span{
  font-size: 25px;
  font-weight: 500;
  color: black;
  margin: 10px 0 15px 0;
}
.drag-area button{
  padding: 10px 25px;
  font-size: 20px;
  font-weight: 500;
  border: none;
  outline: none;
  background: green;
  color: white;
  border-radius: 5px;
  cursor: pointer;
}
# digital-signature//javascript
//selecting all required elements
const dropArea = document.querySelector(".drag-area"),
dragText = dropArea.querySelector("header"),
button = dropArea.querySelector("button"),
input = dropArea.querySelector("input");
let file; //this is a global variable and we'll use it inside multiple functions

button.onclick = ()=>{
  input.click(); //if user click on the button then the input also clicked
}

input.addEventListener("change", function(){
  //getting user select file and [0] this means if user select multiple files then we'll select only the first one
  file = this.files[0];
  dropArea.classList.add("active");
  showFile(); //calling function
});


//If user Drag File Over DropArea
dropArea.addEventListener("dragover", (event)=>{
  event.preventDefault(); //preventing from default behaviour
  dropArea.classList.add("active");
  dragText.textContent = "Upload File";
});

//If user leave dragged File from DropArea
dropArea.addEventListener("dragleave", ()=>{
  dropArea.classList.remove("active");
  dragText.textContent = "Drag & Drop your file";
});

//If user drop File on DropArea
dropArea.addEventListener("drop", (event)=>{
  event.preventDefault(); //preventing from default behaviour
  //getting user select file and [0] this means if user select multiple files then we'll select only the first one
  file = event.dataTransfer.files[0];
  showFile(); //calling function
});

function showFile(){
  let fileType = file.type; //getting selected file type
  let validExtensions = ["image/jpeg", "image/jpg", "image/png"]; //adding some valid image extensions in array
  if(validExtensions.includes(fileType)){ //if user selected file is an image file
    let fileReader = new FileReader(); //creating new FileReader object
    fileReader.onload = ()=>{
      let fileURL = fileReader.result; //passing user file source in fileURL variable
  	  // UNCOMMENT THIS BELOW LINE. I GOT AN ERROR WHILE UPLOADING THIS POST SO I COMMENTED IT
      // let imgTag = `<img src="${fileURL}" alt="image">`; //creating an img tag and passing user selected file source inside src attribute
      dropArea.innerHTML = imgTag; //adding that created img tag inside dropArea container
    }
    fileReader.readAsDataURL(file);
  }else{
    alert("This is not an Image File!");
    dropArea.classList.remove("active");
    dragText.textContent = "Drag & Drop your file";
  }
}
