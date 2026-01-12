# NTUiCal

Python script to parse data from 'Check/Print Courses Registered' to ICS

# Branch Structure

- `main` → stable branch for local use
- `feature-fes` → flask experiments
- `prod-heroku-outdated` → Heroku shuts down free tier
- `prod-render` → deployed to Render

# File Structure

- `server.py` → production server
- `vibe.py` → generate `.ics` from course data
- `groove.py` → converts `.ics` to `.json` for calendar view
- `scrap.py` → prepare HTML data before passing to `vibe.py`

# Input Data Required

- Date of semester's first day according to [NTU Calendar](https://www.ntu.edu.sg/admissions/matriculation/academic-calendars)
- Semester's course data from [Check/Print Courses Registered](https://sso.wis.ntu.edu.sg/webexe88/owa/sso_redirect.asp?t=1&app=https://wish.wis.ntu.edu.sg/pls/webexe/aus_stars_check.check_subject_web2)

# Usage

### 1. Using the Deployed [Site](https://ntuical.onrender.com)

- Select date of semester's first day
    <details>
    <summary>Example</summary>
    <br>
    Monday of Week 1
    <img src="images/get_date.png">
    <img src="images/choose_date.png">
    </details>
- Upload your course data
  - **Option 1:** Upload the `.html` file **[Recommended]**
      <details>
      <summary>Example</summary>
      <br>
      Right Click → Save Page As
      <img src="images/get_html.png">
      <img src="images/upload_html.png">
      </details>
  - **Option 2:** Paste course table data
      <details>
      <summary>Example</summary>
      <br>
      Only copy the contents within the red box
      <img src="images/get_data.png">
      <img src="images/paste_data.png">
      </details>
- Click `Parse` to preview `VEVENT`s
- Click `Download` to obtain the `.ics` file

### **OR**

### 2. Running the [`vibe.py`](fes/vibe.py) Script Locally

- Clone the repository

  ```
  git clone https://github.com/reown/ntu-ical.git

  cd ntu-ical
  ```

- Save your [Check/Print Courses Registered](https://sso.wis.ntu.edu.sg/webexe88/owa/sso_redirect.asp?t=1&app=https://wish.wis.ntu.edu.sg/pls/webexe/aus_stars_check.check_subject_web2) data as
  - a `.html` file or
  - copied to a `.txt` file
  <details>
  <summary>Example</summary>
  See <a href ="samplehtml/">samplehtml</a>
  <br>
  or <a href = "sampletxt/">sampletxt</a>
  </details>
- Install dependencies
  ```
  pip install -r requirements.txt
  ```
- Run the script (requires 2 arguements)
  ```
  python fes/vibe.py <filePath> <DDMMYYYY>
  ```
  - `<filePath>`: path to your `.html` or `.txt` file
  - `<DDMMYYYY>`: date of semester's first day (eg., `09082021`)
- The `.ics` file will be saved in the same directory with the same name as your input file

# Supported Cases

- [x] Exempted Modules
- [x] Online Modules
- [x] Recess Week
- [x] Saturday Classes
- [x] Merged rows (Empty Course/Title)
- [ ] Missing Laboratory Codes (Engineering only?)
- [ ] 'Asynchronous online learning' Remark
- [ ] HTML from STARS
- [ ] Exam Schedule
