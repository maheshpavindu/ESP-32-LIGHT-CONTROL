# ESP-32-LIGHT-CONTROL
ESP32+FIREBASE REALTIME DETABASE AND HOSTING 


කොඩ් එක esp32_firebase_led.ino ෆයිල් එකේ තියෙනවා. GPIO 23 LED එක Firebase එකෙන් on/off වෙනවා.

සකස් කරන හැටි:

Arduino IDE → Library Manager එකෙන් “Firebase ESP Client” (Mobizt) install කරන්න.
Firebase Console එකේ project එකක් හදලා Realtime Database හදන්න.
Authentication → Sign-in method එකේ Anonymous enable කරන්න.
Database Rules එකේ read/write true කරන්න (test කරන්න පමණයි):
   { "rules": { ".read": true, ".write": true } }
Database එකේ led → state කියලා node එකක් හදලා 1 (ON) හෝ 0 (OFF) දාන්න.
කොඩ් එකේ මේවා වෙනස් කරන්න: WIFI_SSID, WIFI_PASSWORD, API_KEY (Project Settings එකේ Web API Key), DATABASE_URL.
Board එක ESP32 Dev Module තෝරලා upload කරන්න.

LED එකේ positive පැත්ත GPIO 23 එකටත්, negative පැත්ත 220Ω resistor එකක් හරහා GND එකටත් සම්බන්ධ කරන්න.


Firebase Console එකේ Realtime Database page එකේදී මෙහෙම කරන්න:

Build → Realtime Database එකට ගිහින් Data tab එක ඇරින්න.
Database URL එකේ (උදා: https://xxxx-default-rtdb.firebaseio.com/) අයිතිය පැත්තේ තියෙන ➕ (plus) icon එක ටැප් කරන්න.
Name කොටසේ led ලියන්න. Value කොටස හිස්ව තියන්න.
ඒ led node එක ඉස්සරහා තියෙන ➕ icon එක ටැප් කරන්න.
Name එකට state ලියලා Value එකට 1 දාන්න.
Add ටැප් කරන්න.

ඉන්පස්සේ ව්‍යුහය මෙහෙම පෙනෙන්න ඕන:

led
 └── state: 1

LED එක ON කරන්න state අගය 1 කරන්න, OFF කරන්න 0 කරන්න. අගය මත ක්ලික් කරලා edit කරන්න පුළුවන්. වෙනස් කළ ගමන් ESP32 එක තත්පරයක් ඇතුළත ඒක කියවලා LED එක මාරු කරනවා.

Rules එකේ read/write true කරලා නැත්නම් ESP32 එකට කියවන්න බැහැ, ඒක Rules tab එකෙන් Publish කරන්න අමතක කරන්න එපා.



led_control.html කියන ලස්සන web page එකක් හැදුවා. ලොකු රවුම් power බටන් එකක් තියෙනවා, ON වෙනකොට කොළ පාටින් දිලිසෙනවා, dark/light mode දෙකටම ගැලපෙනවා.

පාවිච්චි කරන හැටි:

ෆයිල් එක download කරලා, text editor එකකින් ඇරලා DB_URL එකට ඔබේ Firebase Database URL එක දාන්න (උදා: https://xxxx-default-rtdb.firebaseio.com, අගට / එපා).
ෆයිල් එක phone එකේ හෝ PC එකේ browser එකකින් ඇරින්න.
බටන් එක ටැප් කළාම led/state අගය 1 / 0 වෙනවා, ESP32 එක ඒක කියවලා LED එක මාරු කරනවා.

මේ page එක Claude ඇතුළේ කෙලින්ම වැඩ කරන්නේ නැහැ, ඒ නිසා ෆයිල් එක download කරලා ඔබේ browser එකෙන් ඇරින්න ඕන. පස්සේ ඕන නම් Firebase Hosting එකට දාලා ලින්ක් එකක් විදිහට ෆෝන් එකේ ඕනෑම තැනක ඉඳන් පාවිච්චි කරන්නත් පුළුවන්.


Firebase Hosting එකට දාන්න PC එකේ Command Prompt එකෙන් මේ පියවර කරන්න.

1. Node.js install කරන්න

nodejs.org එකෙන් LTS version එක download කරලා install කරන්න. ඉවර වුණාම Command Prompt එකක් අලුතින් ඇරින්න.

2. Firebase CLI install කරන්න

npm install -g firebase-tools

3. Login වෙන්න

firebase login

Browser එකක් ඇරෙනවා. ඔබේ Firebase එකට පාවිච්චි කරන Google account එකෙන් login වෙන්න.

4. Folder එකක් හදලා ඇතුළට යන්න

mkdir led-web
cd led-web

5. Hosting set up කරන්න

firebase init hosting

ප්‍රශ්න වලට උත්තර දෙන්න ඕන මෙහෙම:

Use an existing project තෝරලා ඔබේ project එක තෝරන්න
public directory: public (Enter ඔබන්න)
single-page app?: N
GitHub deploys?: N
index.html overwrite කරන්නද කියලා ඇහුවොත්: N

6. බටන් ෆයිල් එක දාන්න

දැන් led-web folder එක ඇතුළේ public folder එකක් හැදිලා තියෙනවා. ඒකට led_control.html ෆයිල් එක copy කරලා නම index.html කරන්න. (ඒකේ DB_URL එක දාලා තියෙන්න ඕන.)

7. Deploy කරන්න

firebase deploy

ඉවර වුණාම Hosting URL එකක් පෙන්නනවා, මේ වගේ:

https://your-project.web.app

ඒ ලින්ක් එක ෆෝන් එකේ browser එකෙන් ඇරින්න. Home Screen එකට add කරගත්තොත් app එකක් වගේ පාවිච්චි කරන්න පුළුවන්.

firebase command එක PowerShell එකේ “running scripts is disabled” කියලා error එකක් දුන්නොත්, Command Prompt (cmd) එකෙන් කරන්න.

ඒ පියවරෙන් කියන්නේ Command Prompt එකේදී අලුත් folder එකක් හදලා ඒක ඇතුළට යන්න කියලා. cmd එකේ ලියන්න ඕන දේවල් මෙහෙමයි.

ක්‍රමය 1: Command Prompt එකෙන්ම

Windows search එකේ cmd ටයිප් කරලා Command Prompt ඇරින්න.
මේක ටයිප් කරලා Enter ඔබන්න:
   mkdir led-web

මේකෙන් led-web කියන folder එකක් හැදෙනවා. දැනට ඉන්නේ C:\Users\User එකේ නම් ඒක ඇතුළේ හැදෙනවා.
3. ඊළඟට මේක ටයිප් කරලා Enter ඔබන්න:

   cd led-web

මේකෙන් ඒ folder එක ඇතුළට ගියා. දැන් පේළියේ මෙහෙම පේන්න ඕන: C:\Users\User\led-web>

ඉන්පස්සේ ඊළඟ command එක (firebase init hosting) ඒ විදිහටම ටයිප් කරන්න.

ක්‍රමය 2: Folder එක අතින් හදලා

Desktop එකේ right-click කරලා New → Folder තෝරලා නම led-web දෙන්න.
ඒ folder එක ඇරලා උඩ තියෙන address bar එක (path එක පේන තැන) මත ක්ලික් කරන්න.
ඒකේ cmd කියලා ටයිප් කරලා Enter ඔබන්න.
දැන් Command Prompt එක ඇරෙන්නේ ඒ folder එක ඇතුළෙමයි. cd කරන්න ඕන නැහැ.


ඊට පස්සේ මේ පියවර වරින් වර කරන්න. Command Prompt එක led-web folder එක ඇතුළේ තියෙද්දී:

1. Hosting set up කරන්න

firebase init hosting

(firebase command එක වැඩ නැත්නම් කලින් npm install -g firebase-tools සහ firebase login කරලා නැති එකයි. ඒවා කරන්න.)

ප්‍රශ්න වලට උත්තර දෙන්න ඕන මෙහෙම (ඉඳහිට ප්‍රශ්න අනුපිළිවෙල වෙනස් වෙන්න පුළුවන්):

Are you ready to proceed? → Y
Please select an option → ඊතල යතුරු වලින් Use an existing project තෝරලා Enter
ඔබේ project එක තෝරලා Enter
What do you want to use as your public directory? → public ටයිප් කරලා Enter
Configure as a single-page app? → N
Set up automatic builds with GitHub? → N
File public/index.html already exists. Overwrite? → N

2. බටන් ෆයිල් එක දාන්න

File Explorer එකෙන් led-web folder එක ඇරියම ඇතුළේ public folder එකක් හැදිලා තියෙනවා.

led_control.html ෆයිල් එක ඒ public folder එකට copy කරන්න.
කලින් තිබුණ index.html ෆයිල් එක delete කරන්න.
දැම්ම ෆයිල් එකේ නම index.html කියලා වෙනස් කරන්න (right-click → Rename).
ඒ ෆයිල් එක Notepad එකෙන් ඇරලා DB_URL එකට ඔබේ Database URL එක දාලා Save කරන්න.

3. Deploy කරන්න

Command Prompt එකේ:

firebase deploy

ඉවර වුණාම මේ වගේ පේළියක් පෙනෙනවා:

Hosting URL: https://your-project.web.app

ඒ ලින්ක් එක ෆෝන් එකේ browser එකෙන් ඇරින්න. බටන් එක ටැප් කරලා LED එක වැඩ කරනවද බලන්න.


ඔව්, firebase deploy කරන්න ඕන led-web folder එක ඇතුළේ (firebase.json ෆයිල් එක තියෙන තැනින්). public folder එක ඇතුළට ගිහින් නොවෙයි.

හරි තැන තියෙනවද බලන්න:

Command Prompt එකේ පේළිය මෙහෙම අවසන් වෙන්න ඕන:

C:\Users\User\led-web>

(ඔබ folder එක හැදුවේ Desktop එකේ නම් C:\Users\User\Desktop\led-web> වගේ පේනවා.)

හරි තැන නැත්නම්:

File Explorer එකෙන් led-web folder එක ඇරින්න.
උඩ address bar එක මත ක්ලික් කරලා cmd ටයිප් කරලා Enter ඔබන්න.
ඇරෙන Command Prompt එකේ මේක ටයිප් කරන්න:
   firebase deploy

ඒ folder එක ඇතුළේ මේ දේවල් තියෙන්න ඕන:

led-web
 ├── firebase.json
 ├── .firebaserc
 └── public
      └── index.html

firebase.json නැත්නම් firebase init hosting කරලා නැහැ, ඒක මුලින් කරන්න ඕන. ඒ වගේම public ඇතුළේ index.html තියෙනවද, DB_URL දාලා save කරලාද කියලත් deploy කරන්න කලින් බලන්න.









2. firebase login
Browser එකක් open වෙනවා. Firebase project එක හදපු Google account එකෙන් login වෙලා Allow ඔබන්න.
Terminal එකේ “Success! Logged in as ...” කියලා පෙන්නනවා.
3. mkdir led-app && cd led-app
mkdir led-app: led-app නමින් අලුත් folder එකක් හදනවා.
cd led-app: ඒ folder එක ඇතුළට යනවා.
&& කියන්නේ "පළවෙනි එක සාර්ථක වුණොත් දෙවැන්න කරන්න".
Windows PowerShell එකේ && වැඩ නැත්නම් එකින් එක type කරන්න:
  mkdir led-app
  cd led-app
4. firebase init hosting

මේ command එක ඇතුළේ ප්‍රශ්න කීපයක් අහනවා. Arrow keys වලින් තෝරලා Enter ඔබන්න:

ප්‍රශ්නය	උත්තරය
Are you ready to proceed?	Y
Please select an option	Use an existing project
Select a default Firebase project	ඔයාගේ project එක තෝරන්න
What do you want to use as your public directory?	public (Enter ඔබන්න)
Configure as a single-page app?	N
Set up automatic builds with GitHub?	N
File public/index.html already exists. Overwrite?	N

ඊට පස්සේ led-app folder එක ඇතුළේ public folder එකක් හැදෙනවා.

5. HTML file එක දාලා deploy කරන්න
esp32_controller.html file එක led-app/public/ ඇතුළට copy කරලා නම index.html කරන්න (කලින් තිබුණු index.html එක replace කරන්න).
Terminal එකේ (තාමත් led-app folder එක ඇතුළේ):
   firebase deploy --only hosting
අන්තිමට මෙහෙම පෙන්නනවා:
   Hosting URL: https://ඔයාගේ-project.web.app

ඒ link එක browser එකේ open කරන්න, ඔයාගේ web app එක එතන තියෙනවා.

පස්සේ වෙනස් කරන්න ඕන නම්

HTML file එක වෙනස් කළාම public/index.html එකට ආයෙ copy කරලා, led-app folder එක ඇතුළේ firebase deploy --only hosting ආයෙ run කරන්න.

Error ආවොත්
'firebase' is not recognized: terminal එක වහලා ආයෙ open කරන්න, නැත්නම් npm install -g firebase-tools එක හරියට වුණාද බලන්න.
npm: command not found: Node.js install වෙලා නැහැ.
Login වෙන්න බැරි නම්: firebase login --no-localhost try කරන්න.
