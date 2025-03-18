# Tribal-Wars-Credits-Extractor
Extracts Tribal Wars by InnoGames credits from the website into Mobygames import format-ish

# How

 - Go to https://www.tribalwars.net/en-uk/page/credits
 - Open your browser's developer tools
 - Paste the following to the console and return

```js
// Dates Suck Start
// https://stackoverflow.com/a/15397495

const nth = (d) => {
  if (d > 3 && d < 21) return 'th';
  switch (d % 10) {
    case 1:  return "st";
    case 2:  return "nd";
    case 3:  return "rd";
    default: return "th";
  }
};

const todaysdate = new Date(+new Date);
const date = todaysdate.getDate();
const month = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"][todaysdate.getMonth()];

today = `${month} ${date}${nth(date)}, ${todaysdate.getFullYear()}`;

// Dates Suck End
// Inject jQuery Start even though might be not necessary

javascript: (function(e, s) {
    e.src = s;
    e.onload = function() {
        jQuery.noConflict();
        console.log('%c jQuery injected', 'color:red');
        gettribalcredits()
    };
    document.head.appendChild(e);
})(document.createElement('script'), '//code.jquery.com/jquery-latest.min.js')

// Inject jQuery End

function gettribalcredits() {

let supergroup = jQuery('h2').text(); // get group of groups

var credits = {};
var credits_text = '';

jQuery('div.bordered-box').each(function (){

	let group = jQuery(this).find('h3').text();
	
    var title_order = [];
	
	jQuery(this).find('tr').each(function() {
		
		let name = jQuery(this).find('td').first().text();
		let title = jQuery(this).find('td').last().text();
		
		if ( !(group in credits) ) {
			credits[group] = {};
		}
		if ( !(title in credits[group]) ) {
			credits[group][title] = [];
			credits[group][title].push(name);
			
			title_order.push(title);
		} else {
			credits[group][title].push(name);
		}
		
	});
	
	credits_text += '\n' + supergroup + ': ' + group + ' (website credits ' + today + ')\n';
	title_order.forEach(function (title, title_index) {
		credits_text += '\n' + title + '\n';
		credits[group][title].forEach(function (name, name_index) {
			credits_text += name + '\n';
		});
	});
	

});

console.log(credits_text);

}
```
 - drag-select the output text and copy it to Notepad++
 - Remember there are two pages (as of writing this), do the same on the other page ( https://www.tribalwars.net/en-uk/page/team )

Now it's time for manual cleanup:

 - split role titles, e.g. "Managing Director / Visionary Creator"
 - ensure proper cAsE in titles, groups, etc.
 - Protip for group (title case) checking: regex-search repeatedly for `\r\n\r\n^.*$\r\n\r\n`—though this skips the first one if there's no empty line above.
 - handle silly stuff like '🍩 Arjeta Avllaj ☕'
 - Delete the accidental 'join our team' group, obviously
 - Maybe also manually add the copyright info from below the footer
 - take screenshots, see below 

# Screenshot

- Go to https://www.tribalwars.net/en-uk/page/credits
- Avoid using built-in screenshot features and you can do even better than 👍ShareX👍 in this situation, otherwise you have to time the ~~stup–~~ silly scrolling `<marquee>` names, so instead:
- Use browser development tools to double-click-replace `<marquee>` with `<span>` and press return:
- ![demarquee](https://github.com/user-attachments/assets/2cb6afc0-9a8a-4b8a-889b-9367dfedfda6)
- (optional, expert only) use the devtools to delete elements that just waste Kilobytes like the banner and footer links but best keep stuff that clarifies where we are (top navbar) and the copyright stuff at the bottom.
- Make the browser window narrow-ish (just wide enough for most names to only take up one line) and use [GoFullPage chrome screenshot extension](https://chromewebstore.google.com/detail/gofullpage-full-page-scre/fdpohaocaechififmbbbbbknoalclacl) or something similar.
- Remember there are two pages (as of writing this), do the same on the other page ( https://www.tribalwars.net/en-uk/page/team )

# Result

The non-cleaned up results look like this:

## Page 1 output

```
Development team: Current team (website credits March 18th, 2025)

Backend Development
🍩 Arjeta Avllaj ☕
Jon Dawson

Development
Ben Bellmann
Maximilian Lotz

Community Specialist
Christian Jürgensen 

System Administration
German Syomin
Meik Milevczik

Designer
Hans-Arno Wegner

Quality Assurance
Harri Kemppainen

Lead Development
Kai Neuwerth

Office Intern
Thomas Cartwright

Product Management
Thorsten Schankin

Development team: Past contributors (website credits March 18th, 2025)

Designer
Alexander Arndt
Anwar Dalati
Gracie Drake
Mike Dermendjin
Stephan Schwake

Marketing
Alexander Padberg
Anita Böhm
Johannes Klug
Sebastian Goldt
Tobias Fink

External Developers
Alison Simpson
Daniel Stelter-Gliese

Community Specialist
Anahí Mendoza Santillán
Aristeidis Moiras
Chris A.
Jayden Lamb-Pullen
Timo Wienekamp

Lead Community Manager
Andreas Prinz
Timothy Loftus

Graphics
Andrei Pervukhin
Arne Lund
Camilo Arrieta
Helmut Weininger
Jan Lorenz Siepe
Judith Gastell
Kevin Suckert
Oliver Milas

Product Management
Anna Sieprawska
Chase Williams
Karl Stahlmann
Nino Protic
Robert Aiking
Thomas Raimbault

Head of Community Management
Dominika Borgosz

Managing Director / Visionary Creator
Eike Klindworth
Hendrik Klindworth
Michael Zillmer

Mobile Development
Eric Hoffmann
Philipp Bornstedt

Lead Development
Heiko Münz
Lars Tesmer

Frontend Development
Jan-Christopher Schubert
Nils Brüning-Zedler

Quality Assurance
Jana Gierloff

Backend Development
Marcus Harrison
Matthias Dötsch
Michael Indyk
Milan Beran
Nicholas Toby
Ole Michaelis
Oliver Blaha
Sirko Bretschneider
Tobias Rojahn

System Administration
Matthias Klein
Raimund Schlichtiger
Wolf Dieter Rieck

Development team: Community Managers (website credits March 18th, 2025)

Arabic
Alaa

Beta
JawJaw

Brazil
allura
Carla Santos

Czechia
kubina

France
funnette

Germany
katzenmarylou
rauhaa

Greece
purge

Hungary
oldfox

International
JawJaw
Jirki88

Italy
cikketto

Netherlands
kr33log

Poland
jarq
kmic
Oski

Portugal
Ricardo Vitoriano

Romania
rakanishu

Russia
bear

Slovakia
bastelroyce

Spain
ghostt

Sweden
SuperNova

Switzerland
bobydeluxe

Thailand
toon

Turkey
Mr Storm

UK
mellofax

USA
Kawoni
```

See how you have to fix case and split "Managing Director / Visionary Creator"?

## Page 2 output

```
Support team: Team leaders (website credits March 18th, 2025)

Community Manager
mellofax
Nova

Community Manager (TH)
toon

Support team: Team members (website credits March 18th, 2025)

Senior In-Game Supporter & Speed Admin
Basand

Senior In-Game Supporter & HP Admin
Gunnersaurus

In-Game Supporter
Lionguard32
Sebbe

Senior Forum Moderator
Nightfall
Zord Gaf

Senior In-Game Supporter & Script Admin
RedAlert

Support team: Join our team (website credits March 18th, 2025)
```

- I guess "HP Admin" is "Homepage Admin" but WTF is a "Speed Admin"?
- There's plenty to clean up, with "Senior In-Game Supporter" being singular (gotta pluralize) and split among 3 cumulative role titles and all.
- Remember what we agreed on about "Join our team" earlier?

## Screenshots

The clean screenshots look like:

![tribalcred1](https://github.com/user-attachments/assets/4711ea54-b7ce-4b0d-a2a2-fb7024cfcd4a)
![tribalcred2](https://github.com/user-attachments/assets/1a220c99-a1b0-4af4-9432-1629acf230f2)

# Post-cleanup matching

Only two changes were added through matching:

![changes](https://github.com/user-attachments/assets/a8822cd9-bb9c-4da9-8cc9-4f9f6770e3e0)

Here compared on text-compare.com

However there was no evidence the identified individuals were correct, so I had to revert those matches.
