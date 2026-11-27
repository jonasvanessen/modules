# Vim Navigation Cheat Sheet

## File and Line Jumping
| Action | Command(s) |
| :--- | :--- |
| **Go to line `N`** (e.g., line 42) | `42G`, `42gg`, or `:42` + `Enter` |
| **Beginning of file** | `gg` |
| **End of file** | `G` |
| **Jump `N` lines down / up** *(with `relativenumber`)* | `3j` (3 down), `3k` (3 up) |

---

## In-Line and Word Movement
| Action | Command |
| :--- | :--- |
| **Start of line** | `0` |
| **End of line** | `$` |
| **Next word** | `w` |
| **Previous word** | `b` |

---

## Search
| Action | Command |
| :--- | :--- |
| **Search forward (down)** | `/searchterm` + `Enter` |
| **Search backward (up)** | `?searchterm` + `Enter` |

---

## Line Number Display Settings
* **Absolute line numbers:** `:set number`
* **Relative line numbers:** `:set relativenumber`
* **Hybrid mode** *(relative + current line number)*: `:set relativenumber number`

> **Tip:** In Vim, the count always comes **before** the motion (`3j` / `3k`, not `j3` / `k3`).
