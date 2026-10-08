# 🎃 Scratch Project Feedback Speed Dating: Spooky Story Edition

A single-file classroom web app that pairs students for quick, structured peer feedback on their Scratch projects. Spin the wheels, reveal the matchups, run a 2.5 minute countdown with a tolling bell, and repeat for four rounds. At the end you get a summary of exactly who shared with whom, ready for a Learning Journal reflection.

Built for a middle school Computer Programming class, but it works for any project that students can show a partner on a screen.

**Live app:** https://wfryer.github.io/scratch-feedback-speed-dating/spooky-speed-dating.html

---

## ✨ What It Does

- **Setup screen** with an editable class list and tap-to-mark-absent names
- **Fun "ARE YOU READY FOR A SPOOKY STORY?" splash screen** with floating ghosts, bats, and pumpkins
- **Two spinning wheels** (🧙 Sprite Sorcerer and 👻 Script Whisperer) that land on a match, then reveal the full pairing table for the whole class at once
- **Smart pairing rules** so nobody ever works with the same partner twice, and every student gets to share their own project the same number of times
- **Odd class sizes handled** with a group of three (one sharer, two feedback givers) or an optional guest partner
- **Countdown timer** with a "find your partner" phase, a chime when sharing starts, and a tolling bell when time is up
- **Summary screen** with a by-student view and a by-round view, plus Copy, CSV download, and Print buttons
- **Auto-save and resume** in case the browser tab is refreshed mid-class
- **No installs, no accounts, no server.** Everything runs in one HTML file

---

## 🎮 Run a Session in 8 Steps

1. Open `spooky-speed-dating.html` in any modern browser (or use the live link above) and project it for the class.
2. Edit the class list if needed (one first name per line).
3. Tap the name of anyone who is absent. Their chip turns red and they are left out of the pairings.
4. Optional: check **Add a guest partner** if you have an odd number of students. The guest (you, by default named "Teacher") is paired like a student and shares a project too.
5. Click **🕸️ Build the Spooky Schedule**. All four rounds are planned right away.
6. On the splash screen, have students open their Scratch project, then click **🎃 I'M READY! 🎃**.
7. Click **🎃 SPIN FOR ROUND 1**. The wheels spin, then the full matchup table appears. Click **▶ Start Timer** and let the countdown run.
8. When the bell rings, click **Next Round ➜**. After the last round, click **📋 Show Summary**.

---

## 🧩 How the Pairing Works

Every round, students are split into pairs. Each pair has one **Sprite Sorcerer** (the project sharer) and one **Script Whisperer** (the feedback giver). If the number of players is odd, one group of three is formed with one sharer and two whisperers.

The app plans **all rounds up front**, before the first spin, so these rules are guaranteed:

| Rule | What it means |
|---|---|
| **No repeat partners** | Anyone who has been in your group in an earlier round will not be in your group again. In a group of three, all three count as having met. |
| **Fair sharing** | Every student is the Sprite Sorcerer the same number of times whenever the math allows it. |
| **Everyone placed** | Every present student appears exactly once per round. |

The wheels are for suspense. They land on one pre-planned match each round, then the full table is revealed.

### The math behind "everyone shares twice"

With 4 rounds, every student shares twice only when the number of groups per round times 4 equals twice the number of players. That works out perfectly when the number of players is even:

| Players | Groups per round | Sharer slots (4 rounds) | Result |
|---|---|---|---|
| 20 | 10 pairs | 40 | Everyone shares exactly 2 times |
| 16 | 8 pairs | 32 | Everyone shares exactly 2 times |
| 15 | 6 pairs + 1 trio | 28 | 13 students share twice, 2 share once |

If you have an odd class, turn on the **guest partner** option to make the count even. The guest shares a project too, so have one ready.

If the class is very small (fewer players than rounds plus one), some partners must repeat. The app warns you on the setup screen and notes the repeats on the summary screen. You need at least 4 players.

---

## ⏱ Timer and Sounds

The timer counts down from **2:30**.

| Time | What happens |
|---|---|
| 2:30 to 2:00 | 🏃 "Find your partner!" |
| 2:00 | A chime plays and the screen says it is sharing time |
| Under 0:15 | The digits turn orange |
| 0:00 | A four-toll bell rings and the timer flashes "Time is up!" |

You can pause and resume the timer, reset it, or skip ahead to the next round (the app asks you to confirm if the timer has not finished).

All sounds are **synthesized in the browser** with the Web Audio API. There are no audio files to load, so school content filters cannot block them. Browsers require a click before playing sound, so click **I'M READY** first. Use the **🔔 Sound on** button to mute.

---

## 📋 Summary and Export

After any round (and at the end), click **📋 Summary**.

- **By student:** one row per student showing what they did in each round, such as "Shared with Daniel" or "Gave feedback to Emma (with Ben)", plus totals for times shared and times gave feedback
- **By round:** the full matchup table for each round
- **Copy table:** copies a tab-separated table you can paste straight into a Google Doc or Sheet
- **Download CSV:** saves `spooky-speed-dating-matchups.csv`
- **Print:** a clean, print-friendly version

### Learning Journal reflection ideas

The summary makes a great reference for a follow-up reflection. Students can write about:

- Which feedback helped you most, and what did you change because of it?
- What was your favorite idea you saw in someone else's project?
- What is one thing you learned about Scratch from watching a classmate's code?
- What kind of feedback do you want to give more often?

---

## 🛠 Customizing It

Open the HTML file in any text editor and find the `CONFIG` block near the top of the `<script>` section.

```js
const CONFIG = {
  roster: ["Ava", "Ben", "Caleb", ...],   // default class list
  absentByDefault: [],                    // names pre-marked absent
  guestName: "Teacher",                   // name shown for the guest partner
  guestOnByDefault: false,                // start with the guest turned on?
  rounds: 4,                              // number of rounds
  totalSeconds: 150,                      // timer length (150 = 2:30)
  findPartnerSeconds: 30,                 // "find your partner" phase
  bellTolls: 4,                           // how many bell tolls at the end
  sharer: { title: "Sprite Sorcerer", plural: "Sprite Sorcerers", icon: "🧙", desc: "..." },
  giver:  { title: "Script Whisperer", plural: "Script Whisperers", icon: "👻", desc: "..." }
};
```

- **Change the class list:** edit `roster`, or just edit the list on the setup screen each time.
- **Rename the roles:** change the `title`, `plural`, `icon`, and `desc` fields. You can make them fit any theme.
- **Change the timing or number of rounds:** edit `rounds`, `totalSeconds`, and `findPartnerSeconds`. An even number of rounds works best for fair sharing.
- **Restyle the colors:** the `:root` block at the top of the `<style>` section holds the color variables.

The default class list is 20 generic first names so you can try the app right away.

---

## 💡 Classroom Tips

- Have students open their project **before** the first round so no time is lost.
- Do a quick **sound check** and a test spin before class, especially on a new projector or speaker.
- Model what good feedback sounds like first, such as "My favorite part was..." and "One idea to make it even better is...".
- Give the Sprite Sorcerer a goal, like clicking the green flag and explaining one block they are proud of.
- If two students have the same first name, add an initial in the list (for example "Alex M." and "Alex R.").
- Keep the table on screen during each round so students can find partners quickly.
- Closing the tab by accident is fine. Reopen the page and click **Resume**.

---

## 🔒 Privacy

Everything runs locally in the browser. No names or results are sent anywhere. To support the Resume feature, the current schedule is saved in your browser's local storage on that device only. Click **↺ Start over** (or **Discard** on the setup screen) to clear it. Use first names only.

The page loads two fonts from Google Fonts. If your network blocks them, the app still works with system fonts.

---

## 🔧 Technical Notes

- **One file:** HTML, CSS, and vanilla JavaScript in a single `.html` file
- **No frameworks or dependencies**
- **Wheels:** drawn with the HTML5 Canvas
- **Sounds:** Web Audio API, fully synthesized
- **Scheduling:** a randomized search builds each round with a no-repeat constraint, then a capacity-limited matching assigns who shares so the counts stay balanced
- **Saving:** browser local storage
- **Testing:** the scheduling logic was checked across thousands of random class sizes and layouts, and a full simulated class session (setup, four rounds, timer, summary, resume) was run in a test browser. Please still do a quick dry run on your own projector and speakers.

---

## 📁 Files

```
spooky-speed-dating.html   The entire app
README.md                  This file
```

To publish it yourself, put both files in a GitHub repo and turn on **Settings, Pages, Deploy from a branch, main**. Your app will be live at `https://YOUR-USERNAME.github.io/YOUR-REPO/spooky-speed-dating.html`.

---

## 🙏 Credits

Vibe coded by [Dr. Wes Fryer](https://github.com/wfryer/) with help from [Claude](https://claude.ai) (Anthropic).

- More projects on GitHub: https://github.com/wfryer/
- More AI learning: https://ai.wesfryer.com

Related classroom tools:

- [spooky-story](https://github.com/wfryer/spooky-story): a three-wheel "Spin a Spooky Story" idea generator for the Spooky Scratch Story project
- [creature-spin](https://github.com/wfryer/creature-spin): a mythological creature spinner

---

## 📄 License

Feel free to use, modify, and share this freely for educational purposes. A credit link back is appreciated but not required.
