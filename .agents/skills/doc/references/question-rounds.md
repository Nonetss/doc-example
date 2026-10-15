# Question rounds

To finish documenting a whole section (network, backups…) in one go, run a
**question round**: whoever writes (a person or an agent) prepares the
questions, whoever knows the topic answers them roughly, and the writer moves
the answers into the pages. It closes a section in one sitting instead of open
question by open question.

With Claude Code, **`/questions <section>`** (for example `/questions backups`)
writes the questions. Once they are answered, **`/questions`** again moves the
answers into the pages.

## How it works

1. **Review the section.** Read its pages, their `open_questions` and any
   "_Pending…_" line in the text, and search the rest of `docs/` and
   `catalogo/` for what is already answered, so it is not asked again.
2. **Write the questions** in `questions.md` at the repository root (not under
   `docs/`: it is not documentation). Three lines of instructions on top, then
   the questions grouped by topic, what breaks first going first. Each
   question in bold, with an empty `>` line under it for the answer:

   ```markdown
   # Questions: Backups

   Answer under each one, roughly. If you don't know or don't care, write
   "don't know" or "doesn't matter" and it will be dropped. If someone else
   owns it, write their name.

   ## 1. Duplicati

   1. **Restore test.** Has a full backup ever been restored? Paste the output
      of `ls -la /mnt/nas/backups` on the NAS.

      >
   ```

3. **Answer** under each `>`, however it comes: loose sentences, terminal
   output pasted as is, or the path of a screenshot left at the repository
   root.
4. **Move the answers into the pages:**
   - Each answer goes to the page it belongs to, written cleanly and without
     naming who answered.
   - **The open question is closed completely**: removed from the header and
     the text, with no leftover turned into a new open question.
   - **A blank answer, or "doesn't matter" / "don't know", closes it too**, and
     it is never asked again.
   - **"Someone else owns it"** becomes one line saying who runs it, and
     nothing more.
   - When an answer can be read two ways, write the most sensible reading and
     say which one was chosen, so it can be corrected.
   - Screenshots go to the `img/` folder of the service that uses them.
5. **Close the section.** When it has no open questions left, set `status:
   documented` on its services in `catalogo/services/`, check that every YAML
   still validates, and delete `questions.md`.

## What to ask and what not

These are handover docs for whoever comes next, **not an audit**. Ask **how
something is done and where it is**, not whether it is done right.

| Ask | Don't ask |
| --- | --- |
| What breaks when someone leaves: personal accounts, keys only one person knows | Misconfigurations: a mistyped address, a relay, space that doesn't add up |
| How something is done: restoring a backup, creating a machine, getting into a server | Maintenance chores: reboots, old kernels, repositories, nearly full disks |
| Where something is: a key, a folder, a console | What someone else owns: noting that they run it is enough |
| What something is for, when looking at it doesn't tell | Details everyone picks up with time |

Also:

- **Few, specific questions** (around 15 at most), each with just enough
  context to answer without opening the page.
- **If a fact comes out of a command, ask for the command's output**, not for
  an interpretation of it.
- **What can be looked up in another page or the catalog is looked up**, not
  asked.
- **Never ask for a secret's value.** Ask where it is stored and which account
  uses it.
