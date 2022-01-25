<div align="center">
<h2>Ping Your Heroku Website with Google Scripts!</h2>
<p>Want to keep your free Heroku website alive during business hours?</p>
<p>No problem! We can do that with Google Docs (Spreadsheets) and Google Scripts!<p>
</div>
<br>

<h3 align="center">Step 1: Open Google Docs<h3>
<p><a href="https://docs.google.com/spreadsheets/" target="_blank">Click here</a> to open Google Spreadsheets (login required).</p>
<p>Click on "Blank" under "Start a new spreadsheet." It should open the new spreadsheet on a new tab.<p>
<br>

<h3 align="center">Step 2: Set up Google Spreadsheet</h3>
<p>On the new spreadsheet, place a number '1' on tile B1. This can be any number greater than zero. However, whatever number you put will change where the first run log will print (more on this later).</p>
<p>Afterwards, go to Extensions -> Apps Script. It will open a new tab containing an empty script.</p>
<br>

<h3 align="center">Step 3: Set up Script</h3>
<p>On the new tab, you should see an empty function. Replace the empty function with this:</p>
</div>
<pre>
<code>
function myFunction() {
 let d = new Date();
 let hours = d.getHours();
 let currentTime = d.toLocaleDateString();
 let counter = SpreadsheetApp.getActiveSheet().getRange('B1').getValues();

if (hours >= 8 && hours <= 16) {
let response = UrlFetchApp.fetch('your heroku url here');
}

SpreadsheetApp.getActiveSheet().getRange('A' + counter).setValue("Visted at " + currentTime + " " + hours + "h");
SpreadsheetApp.getActiveSheet().getRange('B1').setValue(Number(counter) + 1);
}
</code>

</pre>

<p>All you need to do is to replace 'your heroku url here' with your actual heroku url (ex. 'https://test-app.herokuapp.com/').</p>
<p>You can add more urls by adding another line inside the if statement (let response2 = UrlFetchApp.fetch('https://test-app2.herokuapp.com/''))
<p>Hours are in PST. You can change the hours according the time you prefer the application to stay awake.</p>

<br>
<h2 align="center">WARNING:</h2>
<p>Please set an appropriate amount of hours based on how much applications and free dynos you have each month. You might risk exceeding your free dynos for the month (which will keep your website down until the next month starts).</p>
<br>

<p>To test if it works, save the function and run it once. You will receive an Authorization notice. Click "Review Permissions," click on your google profile, and click "Allow."<p>
<p>Note: You might get a warning about this being unsafe. Click on Advanced and click "Go to Untitled Project(unsafe)" to go to the next step. This is normal. You are using google applications to run this and in no way is your account in any danger.</p>
<p>After the Authorization, you should see the execution log below print the following:</p>

<pre>
<code>
6:34:03 PM	Notice	Execution started
6:34:03 PM	Notice	Execution completed
</code>
</pre>

<p>This means that your code is working. To verify if it pinged your website, you can remove the response line outside of the hours (in case you are doing this outside of the time range you set) and run the code once. Wait ~30 seconds and see if your website loads instantly. You can also check the google spreadsheet. On A1, it should say 'Visted at {date} {time}'</p>
<br>

<h3 align="center">Step 4: Set Time Trigger</h3>
<p>On the left sidebar of scripts, click on "Triggers."</p>
<p>At the bottom of the page, click "+ Add Trigger."</p>
<p>On the window that appears, change "Select Event Source" to "Time-Driven."</p>
<p>On type of time, select minutes timer. Change minute interval to 15 minutes afterwards.</p>
<p>Save the trigger. It should start running the script every 15 minutes to keep your website awake.</p>
<p>To see if the trigger worked, check if the google spreadsheet adds visit logs on column A.</p>

<h3 align="center">Notes</h3>
<p>I will add further explanations on how this works in the future.</p>
<p>Having issues? Send me a message through LinkedIn <a href="https://www.linkedin.com/in/john-elijah-revan-fajardo-33a189a3/" target="_blank">here</a>.</p>

<div align="center">
</div>
