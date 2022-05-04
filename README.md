html part*


<!DOCTYPE html>
<html lang="en">

<head>
    <link rel="icon" href="boardImg.png">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" />
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
    <link rel="stylesheet" href="./project.css">
    <title> Task Board</title>
</head>

<body id="body" onload="onPageLoad()">
    <h1 id="titelh1" class="animate__animated animate__pulse">My task board</h1>
    <div class="form">
        <div class="animate__animated animate__pulse">
            <label for="taskData">Task Data:</label><br>
            <textarea name="comment" id="taskData" form="taskData" rows="5" cols="80"
                placeholder="Enter free text here..."></textarea> <br>
            <label  for="dueDate">Task Finish Date:</label><br>
            <input type="date" id="dueDate"><br><br>
            <label for="TargetTime"> Task Finish hour:</label><br>
            <input type="time" id="TargetTime"><br><br><br>
            <button onclick="clearFields()" type="reset">Reset </button>
            <button onclick="addNote()" type="submit"> Save note </button>
        </div>
    </div>
    <div id="display"></div>
    <script src="./project.js"></script>
</body>

</html>

javascript part*


  let display = document.getElementById("display")
        let taskData = document.getElementById("taskData")
        let dueDate = document.getElementById("dueDate")
        let TargetTime = document.getElementById("TargetTime")
        let Notes = []

        myValidation = () => {
            let currentTime=new Date
            let isValid = true;
            if(!dueDate.value || !TargetTime.value || currentTime.getTime() > dueDate.valueAsNumber + TargetTime.valueAsNumber + new Date().getTimezoneOffset() * 60 * 1000){
                alert("You must enter a future date");
                isValid = false
            }

            if (taskData.value == ""){
                alert("You must filled all");
                isValid = false
            }

            return isValid
        }
        addNote = () => {
            if (myValidation()) {
                
                let tempTask = { taskData: taskData.value, dueDate: dueDate.value, TargetTime: TargetTime.value }
                Notes.push(tempTask)
                console.log(Notes)
                clearFields()
                saveToLocaleStorage()
                loadFromLocaleStorage()
                notesDisplay()
            }
          
        }
        clearFields = () => {
            taskData.value = ""
            dueDate.value = ""
            TargetTime.value = ""
        }
        delItem = (i) => {
            Notes.splice(i, 1)
            notesDisplay()
            localStorage.setItem("Notes", JSON.stringify(Notes));

        }
        saveToLocaleStorage = () => {
            localStorage.setItem("Notes", JSON.stringify(Notes))
            notesDisplay()}
  
        notesDisplay = () => {
            display.innerHTML = ""
            Notes.forEach( (item, i )=> {
                display.innerHTML += `
                <div class="flexible">
                <div class="animate__animated animate__bounce animate__backInDown">                                                    
                     <div class="displayImg">
                        <button class="delitBtn" onclick="delItem(${i})">X</button>            
                         <p class="text" style="height="30px;" >${item.taskData}</p>
                         <div class="timedate">
                         <p class="card-text">${item.dueDate}</p>
                         <p style= "color: rgb(177, 77, 77);">${item.TargetTime}</p>
                         </div>
                     </div>
               </div>
               </div>`
            })
        }
    

    loadFromLocaleStorage = () => {
        Notes = JSON.parse(localStorage.getItem("Notes")) ?? [];
    }

    onPageLoad = () => {
        loadFromLocaleStorage()
        notesDisplay()
    }
    
    
    style part*
    
    
    
    *{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}
#display {
    display: flex;
}
#body {
    background-image: url(./boardImg.png);
    background-position: center;
    background-size: cover;
    position: absolute;
}

#titelh1 {
    margin-left: 630px;
    font-style: italic;
    padding: 20px;
    font-weight: 200px;

}

.form {
    background-image: url(./shorot.jpg);
    background-repeat: no-repeat;
    border-radius: 100px;
    text-align: center;
    margin-left: 400px;
    margin-right: 50px;
    padding: 70px;
}

.delitBtn {
    border-radius: 50%;
    display: none;
    width: 30px;

}

.displayImg {
    background-image: url(./note.jpg);
    background-repeat: repeat;
    position: relative;
    width: 300px;
    height: auto;
    min-height: 300px;
    padding-left: 35px;
    padding-top: 10px;
    padding-bottom: 5px;         
    margin: 50px;
    background-size: 300px, 500px;
    font-weight: bold;
    
}

.text {
    padding: 15px;
    overflow-wrap: break-word;
}

.card-text {
    color: rgb(177, 77, 77);
}

.timedate {
    position: absolute;
    bottom: 0;
}

.displayImg:hover  .delitBtn {
    display: block;
}

button{
    background-color: rgb(55, 0, 255);
    border-radius: 10px,10px,10px,10px;
}


and properties*
