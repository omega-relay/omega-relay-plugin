# Troubleshooting

Every error is one sentence for the user and a `code`. Do not work around an error with another connector or a local tool.

| Code | What it means | What the user can do |
| --- | --- | --- |
| `NO_COMPUTER` | This connection has no computer it can use: none was given to it, or the owner paused it. | Give this assistant a computer, or resume it, in Omega Relay. |
| `COMPUTER_REQUIRED`, `COMPUTER_NOT_FOUND` | Several computers, or a name that is not one of them. | Pass a name from `list_computers`. |
| `GRANT_REQUIRED` | This connection was not given that part of the capability on that computer. | Give this assistant that part, or Full access, in Omega Relay. |
| `SCOPE_REQUIRED` | The connection was approved for reading only. | Reconnect and allow changes. |
| `USAGE_LIMIT` | The account has used this week's tool calls. | Wait until they reset on Monday at 00:00 UTC. |
| `TOOL_NOT_ON_DEVICE` | The capability is not installed there yet. | Wait for setup to finish in the Omega Relay app. |
| `DEVICE_OFFLINE` | The computer is not connected. | Open the Omega Relay app on it. |
| `NOT_DELIVERED` | The computer went offline before the call reached it. It did not run. | Nothing. Call the tool again once it is back. |
| `DEVICE_CAPABILITY_NOT_READY`, `EXECUTION_SAFETY_NOT_READY`, `GRANT_SCHEMA_DRIFT`, `RESULT_SCHEMA_REQUIRED`, `RESULT_SCHEMA_MISMATCH` | The capability on that computer is not running properly or needs an update. | Update the Omega Relay app. |
| `NEEDS_YOU` | The capability needs the user to do one thing on the computer first. `next` names it and the sentence says it. | Do that step on the computer. |
| `TURNED_OFF`, `NOT_AVAILABLE` | The capability is switched off, or cannot be used on that computer. | Turn it on in the Omega Relay app on that computer, or update the app if the sentence says so. |
| `NO_ANSWER` | The computer did not answer a read in time. Nothing changed. | Nothing. Call the tool again. |
| `OUTCOME_UNKNOWN` | The action may have run. | Nothing yet. Use `check_result`. Do not repeat it. |
| `INVOCATION_NOT_ISSUED`, `INVALID_REQUEST_ID` | That is not a request id, or not one of this connection's calls. | Nothing. Use the id a call returned, or call `check_result` with no id. |
| `RESULT_LOOKUP_UNAVAILABLE` | Relay could not look up that result just now. | Nothing. Ask again with the same request id. Do not send the call again. |
| `AUTHORIZATION_UNAVAILABLE`, `ALLOWANCE_UNAVAILABLE`, `EXECUTION_SIGNER_NOT_READY` | Relay could not check or authorize the call just now. Nothing was sent. | Try again in a moment. If it persists, contact support. |
| `AUTHORIZATION_EXPIRED` | The call reached the computer too late and was not carried out. | Nothing. Call the tool again. |
| `DEVICE_REFUSED` | The computer itself said no, such as for a folder outside what it allows. Its reason is passed on as written. | Follow the sentence in the Omega Relay app. |
| `BROWSER_SESSION_CHANGED`, `BROWSER_SESSION_CHANGED_OR_EXPIRED`, `TAB_NOT_SHARED` | Chrome's connection or the tab changed after it was listed. The call was not carried out. | Nothing. Call `browser_tabs` and use the new ids. |
| `SHARE_A_TAB_FIRST` | Chrome on that computer is not connected to this assistant yet. | Nothing. Call `browser_tabs`, which connects it. |
| `SHARE_A_TAB_IN_CHROME` | No tab is shared with this assistant yet. | Share a tab in Chrome on that computer. Then call `browser_tabs`. |
| `STALE_SNAPSHOT` | The page changed since the snapshot. | Nothing. Take a new snapshot. |
| `URL_NOT_ALLOWED` | Only `http` and `https` addresses can be opened. | Nothing. Use such an address. |
| `KEY_NOT_ALLOWED` | That key cannot be pressed. | Nothing. Use a letter, a digit or a named key such as Enter. |
| `BROWSER_CONNECTION_LIMIT` | Too many assistants are connected to Chrome on that computer. | Disconnect one in Chrome. |
| `SCREEN_CHANGED` | The windows changed after they were listed. The call was not carried out. | Nothing. List the windows again. |
| `OWNER_LIVE_VIEW` | Only the owner starts a live view of the screen, from the web. Looking and acting need nothing started. | Nothing. Use `screen_snapshot`, then act. |
| `INVALID_SCREENSHOT_RESULT` | The picture the computer sent could not be used. | Nothing. Take the picture again. |
| `FILES_REQUIRED` | Putting a file into an app by its path needs Files on that computer. | Give this assistant Files there, or use a kept capture. |
| `JOB_LIMIT` | The computer already keeps as many background jobs as it can. | Nothing. Clear finished ones with `cancel_job`. |
| `SAME_COMPUTER` | A share needs two different computers. | Nothing. Choose another one. |
| `SHARE_NOT_FOUND` | This connection has no share with that id. | Nothing. Use the id `share_files` returned. |
| `SHARING_UNAVAILABLE` | Sharing between computers is not available on Relay right now. | Try later. |
| `INVALID_TOOL_ARGUMENTS`, `TOOL_ARGUMENT_LIMIT` | The arguments do not fit the tool. | Nothing. Correct the call. |
| `RATE_LIMITED` | Too many calls in a short time. | Nothing. Wait, then continue. |
| `MCP_OUTPUT_LIMIT` | The result was too large. | Nothing. Ask for less: fewer lines, a smaller page. |

For capabilities the user added:

| Code | What it means | What the user can do |
| --- | --- | --- |
| `CAPABILITY_NOT_FOUND`, `OPERATION_NOT_FOUND` | That computer has no added capability, or no operation, with that name. A built-in capability is not one. | Nothing. Call `list_capabilities` for the names, or use the built-in tools. |
| `CAPABILITY_NOT_APPROVED` | Nobody has approved it yet. | Approve it in Omega Relay, or agree in chat if this assistant has Full access. |
| `CAPABILITY_CHANGED` | It changed since it was listed. | Review and approve it again. |
| `CAPABILITY_REJECTED` | The owner rejected it. | Only the owner can change that, in Omega Relay. |
| `FULL_ACCESS_REQUIRED` | This assistant may not approve capabilities there. | Approve it in Omega Relay. |
| `INPUT_SCHEMA_NOT_CLOSED`, `LIFECYCLE_OPERATION` | Relay will not send that operation as it is declared. | Its author changes the capability. |

A tool that was listed earlier and is gone now means access, installation or the computer's own settings changed. Call `list_computers` again.

A result from `check_result` is the computer's own answer to that one call. Ids in it are not the ids the tools take: list the tabs or windows again to get those.
