<div align="center">
<h3>Ping Your Heroku Website with Google Scripts!</h3>
<p>Want to keep your free tier Heroku website alive during business hours?</p>
<p>No problem! We can do that with Google Docs (Spreadsheets) and Google Scripts!<p>
<br>
<br>
<h4>Step 1: Open Google Docs<h4>
<p><a href="https://docs.google.com/spreadsheets/">Click here</a> to open Google Spreadsheets (login required).</p>
<p>Click on "Blank" under "Start a new spreadsheet." It should open the new spreadsheet on a new tab.<p>
<br>
<br>
<h4>Step 2: Set up Google Spreadsheet</h4>
<p>On the new spreadsheet, place a number '1' on tile B1. This can be any number greater than zero. However, whatever number you put will change where the first run log will print (more on this later).</p>
<p>Afterwards, go to Extensions -> Apps Script. It will open a new tab containing an empty script.</p>
<br>
<br>
<h4>Step 3: Set up Google Scripts</h4>
<p>On the new tab, you should see an empty function. Replace the empty function with this:</p>
</div>
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

<p>The language is JavaScript with some built-in Google Scripts functions. All you need to do is to replace 'your heroku url here' with your actual heroku url (ex. 'https://test-app.herokuapp.com/').</p>

<div align="center">
</div>
