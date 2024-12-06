This applescript will scrape the presenter notes out of a Keynote presentation and put them into a new TextEdit document.

```
tell application "Keynote"
	activate
	if not (exists document 1) then error number -128
	tell the front document
		set thisDocumentName to the name of it
		set the combinedPresenterNotes to ¬
			"PRESENTER NOTES FOR: “" & thisDocumentName & "”" & return
		repeat with i from 1 to the count of slides
			tell slide i
				if skipped is false then
					set the combinedPresenterNotes to ¬
						combinedPresenterNotes & return & return & presenter notes of it
				end if
			end tell
		end repeat
	end tell
end tell

tell application "TextEdit"
	activate
	make new document with properties {text:combinedPresenterNotes}
end tell
```