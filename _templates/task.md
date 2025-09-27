<%* 
let title = await tp.system.prompt("Task", "", false)
if (!title) {
	return;
}

const folderName = "projects";   
const allFiles = app.vault.getFiles();   
const filesInFolder = allFiles.filter(file => file.path.startsWith(folderName + "/")).map(file => {    
		return file.basename;
	})//.sort((a, b) => a.tolowercase().localecompare(b.tolowercase())); 

/*const fileList = filesInFolder.map(file => {    
		return file.basename;
	}).sort((a, b) => a.tolowercase().localecompare(b.tolowercase()));*/

let fileLinks = filesInFolder.map(file => {return '"[[' + file + ']]"'})
let project = await tp.system.suggester(filesInFolder, fileLinks)

if (!project) { // choose General if no project is chosen
	project = '"[[General]]"'
}
-%>
---
priority: 2
project: <%* tR += project %>
date: <% tp.date.now() %>
type: "[[Tasks]]"
done: false
tags:
link:
created: <% tp.date.now() %>
---

<% tp.file.move("tasks/"+title) %>