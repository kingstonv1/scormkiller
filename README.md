# scormkiller

Method that works to bypass SOME Scorm LMS APIs, for defensive and educational purposes.

Many LMS systems use a backend called SCORM which tracks learning progress. Additionally, these platforms frequently have controls that prevent people from skipping forward before they've had a chance to watch the videos or interact with the games. This is a simple method to manually update the state of the LMS to complete the modules faster.

Load into your LMS and open the developer tools with Ctrl+Shift+C or right click and hit "Inspect Element."
Click on the "Console" tab.
<img width="1920" height="910" alt="image" src="https://github.com/user-attachments/assets/329ccac8-41e9-4f29-a09d-43cb6f2e1523" />

Click on the dropdown menu to change the DOM context from "top" to "ScormContent"
<img width="1014" height="438" alt="image" src="https://github.com/user-attachments/assets/5e8ecf8c-2fe6-4aef-b596-3ae6ab156294" />

Next, click on the video to start the module. Once the module is started, click on the arrow and paste the following script.
```js
try {
    SCORM2004_Initialize(); SCORM2004_SetScore(100, 100, 0);

    if (typeof SCORM2004_SetPassed === 'function') {
        SCORM2004_SetPassed();
    } else if (typeof SCORM2004_SetCompleted === 'function') {
        SCORM2004_SetCompleted();
    }

    SCORM2004_CommitData();
    SCORM2004_Finish("FINISH", true);
    console.log("Course completion successfully falsified and submitted.");
} catch (err) {
    console.error("Error executing SCORM overrides:", err);
}
```

Chrome DevTools will give you a disclaimer about pasting content that you don't understand into the console. They're right, you should be careful about that. It's dangerous. :)

Anyways, type "allow pasting" and hit enter. Then paste the script and hit enter again. You should get a message that says "Course completion successfully falsified and submitted." Back out to your summary page and check your course. It should be marked as completed :*)
