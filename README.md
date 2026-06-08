# 🐓 SUDOKU — Le Coq Francis

A Sudoku game starring **Francis the Rooster**, built as a Telegram Mini App for the **$FRANC** community. Solve grids, climb the ranks in Competition mode, and earn virtual $FRANC.

The whole game is a **single self-contained `index.html`** file — all images are embedded as base64, so there are no external asset dependencies.

---

## 🎮 Features

### Main menu
Three buttons plus a language switch:
1. **Single Grid** — always unlocked (green).
2. **Competition** — green with an open padlock for $FRANC holders, orange with a closed padlock otherwise. Tapping it while locked shows a "holders only — connect your wallet" message.
3. **Connect Wallet** — redirects to the wallet page.
4. **Language flags** — French 🇫🇷 and English 🇬🇧 side by side. The choice is saved locally.

A floating **pilot rooster** sits at the top above the **SUDOKU** title on every menu screen.

### Two game modes

**Single Grid** (one-shot, no scoring)
- 5 difficulties: **Very Easy**, **Easy** (open to everyone), **Medium**, **Hard**, **Very Hard** ($FRANC holders only).
- Free input with no live error detection. The player fills the grid and presses **Validate** — win or lose, that's it.
- Each level button is green/open-padlock if unlocked, orange/closed-padlock otherwise.

**Competition** ($FRANC holders only)
- Climb the ladder from Very Easy to Very Hard, earning virtual $FRANC.
- **3 lives.** A wrong digit costs one life.
- Live error checking: a wrong digit flashes, you lose a life, and the digit is cleared.
- "Resume" and "New Game" submenu, with the **Top 3 scores** displayed below.

### 💰 Economy (Competition only)
| Action | $FRANC |
|---|---|
| Starting balance (first ever game) | **200** |
| Grid won | **+600** (flat, regardless of time or lives) |
| Hint | **−200** (max **4 hints per grid**) |
| Counter help (counts remaining digits, lasts the whole run) | **−400** |

The balance never goes below 0. The **Top 3 scores** are ranked by the $FRANC earned in a single run and saved locally.

### 🐔 Rooster reactions
- **Pilot rooster** — small floating mascot during play.
- **Heart-eyes rooster** — big "BRAVO!" on a grid win; floats for 30 seconds.
- **Astonished rooster** — floats for 30 seconds when a hint is used.
- **Crying rooster** — floats for 30 seconds when a life is lost; also the big Game Over visual.

### 💥 Defeat sequence (both modes)
When a game is lost:
1. Wrong digits blink **red** for 3 seconds.
2. They **fade out** over 2 seconds.
3. The correct solution is revealed in **bold green** for 5 seconds.
4. **GAME OVER** modal with the crying rooster (plus the $FRANC earned, in Competition mode).

### 🎨 Board design
- Dark-purple cells, white digits.
- Three border weights: thin lines between cells, medium lines around each 3×3 box, and the thickest border around the whole grid.
- Selecting a cell highlights its **row, column and 3×3 box** so the player sees the impacted area; matching digits are highlighted separately as a thinking aid.
- Counting of used digits is **off by default** (available only via the paid Counter help in Competition).

### 💾 Saves (all local)
- Top 3 competition scores.
- In-progress competition game (for "Resume").
- Persistent $FRANC balance.
- Language preference.
- Last known holder status (cached).

---

## 🔌 Wallet / $FRANC detection

Holder status is detected through the existing wallet backend, the same one used by the connect-wallet app:

- On load, inside Telegram, the game POSTs the Telegram `initData` to `BACKEND/check-franc`.
- If the response reports a linked wallet holding $FRANC, the player is flagged as a **holder** and Competition + all difficulties unlock.
- The result is cached in `localStorage` so the state survives reloads.

🐓 *Cocorico!*
