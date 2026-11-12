# sachahjkl/ShojiWM, branch `integration`

This branch is upstream `main` (bea4dev/ShojiWM) with fixes that wait for review. Each fix
lives on its own branch; this branch only merges them. When a fix is merged upstream, its
branch leaves this list and `integration` is rebuilt on the new `main`.

| Branch | Pull request | What it changes |
| --- | --- | --- |
| `fix/foreign-toplevel-on-first-buffer` | to open, after a test | A toplevel shows on taskbars from its first buffer, not from its role: a program started hidden has no button. |
| `fix/dmabuf-feedback-unchanged` | to open, after a measurement | A surface's dmabuf feedback is sent only when it changes: smithay's `set_feedback` compared the format tables on every frame ([#185](https://github.com/bea4dev/ShojiWM/issues/185)). |
| `fix/resize-no-stretch` | to open | A forced slot larger than the client's buffer keeps the buffer at its own size, its edge texels filling the rest: a window that grows faster than its client draws is no longer stretched. |
| `fix/foreign-toplevel-on-client-exit` | to open | A toplevel's taskbar handles close when its client disconnects, even if `space.refresh()` dropped the dead window first: no ghost button or thumbnail. |
| `feat/decoration-middle-click` | to open | `onMiddleClick` on decoration nodes: a press of the middle button runs it, so a tab can close on a middle click. |
| `fix/xwayland-stale-display-lock` | [#229](https://github.com/bea4dev/ShojiWM/pull/229) | A display lock left by a process that is gone is taken back, as Xorg does: killed sessions no longer use up the displays tried, which made the embedded satellite fall back to the built-in Xwayland ([#190](https://github.com/bea4dev/ShojiWM/pull/190)). |
| `fix/plasma-stacking-order` | [#232](https://github.com/bea4dev/ShojiWM/pull/232) | Plasma window management clients get the stacking order windows are drawn in, not their creation order: a screenshot tool framing the window under the pointer no longer picks one that is behind another. |
| `fix/focus-during-client-destroy` | — | Keyboard focus changes asked while a toplevel's destruction is handled wait for the next turn of the event loop: a client that disconnected with the keyboard, while the config gave it to another window, made the compositor abort (a `leave` sent to its gone `wl_keyboard`). |

Merged upstream: #184, #186, #187, #189, #192, #194; `WaylandWindow.foreignToplevelId` replaces
the fork's `toplevelIdentifier`. Closed: #191, and #190 left open for the investigation above.
