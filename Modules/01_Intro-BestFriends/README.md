# 01_Intro and "Best Friends"

## PowerShell Story
PowerShell was invented to be a port of ksh for intel to do CPU development with Microsoft. When Intel abandoned the project, Jeffery Snover had a vision for a general purpose admin language for the Microsoft environment. Snover took a pay cut and found an unlikely ally in the MS Exchange team and soon the Monad Shell was born, along with Snover's famous [Monad Manifesto](https://www.jsnover.com/Docs/MonadManifesto.pdf). Envisioned in the document was the need for an object oriented shell that would fuel automation within the Windows ecosystem. After initial launch of Windows PowerShell 1.0 in 2006, we are now currently on cross-platform PowerShell 7.2. PowerShell is the very thing that has enabled Microsoft to build robust offerings like O365 and Azure.

## Everything's an Object
One of PowerShell's main problems to solve, is having to deal with text based terminals. If you end up having to ever use 'sed' or 'awk' in the Linux world, it's because commands tend to produce a text wall that you will have to turn back into an object in order to do anything useful with. This can be referred to as "Prayer based parsing" ("I hope I got the number of tabs right and that the developer doesn't update their output column order"). Why go from an object based input, to an object based return, only to just give the result back as an inflexible wall of text?

### Best Friend #1 - 'Get-Member'

```PowerShell
    # Make a string and save as a variable called 'stuff' and a second variable called 'thing' that is just a number.

    $stuff = "A string of words and such"
    $thing = 42

    # Examining our objects
    $stuff | Get-Member
    $thing | Get-Member

```
- What type of object is $stuff?
- What type of object is $string?

### Best Friend #2 - "Dot Sourcing"
Did you notice that $stuff and $string had a bunch of members? Members can be "Properties" or "Methods". 
- Properties can be single value strings, or even objects, with their own sub-objects (insert Xzibit meme).
- Methods are like built in scripts that can be run against an object sometimes changing the object itself.

You can call either of these by placing a dot '.' after the variable and typing the name of the property or method you want to call.

```PowerShell
$today = Get-Date
$today | Get-Member
$today.DayofWeek
$today.DayofYear
$today.AddDays(7)

(Get-Date).AddDays(7)


```
- CHALLENGE: What day is 180 days away? 
- DOUBLE CHALLENGE: What time is the above number in UTC?

### Best Friend #4 - "Get-Help"
Sometimes I can't even remember my own kids names, or at least I call them the wrong name a lot. How am I supposed to learn a bunch of commands AND what all their parameters are?! 
In PowerShell you don't have to remember things. Snover often says "PowerShell exists the way it does because I am a flawed human being." So relax and use the built in help system.

```PowerShell
# How do you get a list of all cmdlets dealing with processes?

Get-Help -Name *process*
# Same thing as

# How do you use the Get-Process cmdlet?

Get-Help Get-Process -examples

# get the online help page
help Get-Process -online

# show popout window
help get-process -showwindows

# Notice how we switched the command from Get-Help to help and it still worked? (interdasting...)

```

### Best Friend #5 - TAB COMPLETE
Don't commit commands to memory, don't commit commands to memory, don't commit commands to memeory. (get the point?)
Instead, use tab completion to get where you want to go.

```powershell
# Type the following
Get-Pr

# <Press TAB> until you get to Get-Process, if you miss it, go backwards with Shift + TAB

# Type the Following
Get-Process -

# <Press TAB> to see all the parameters of the command.
```

- CHALLENGE :: Open Google Chrome and several tabs. Store the process object(s) for "Chrome" in a variable called 'oink'.

- DOUBLE CHALLENGE :: Kill ALL the chrome processes. (Hint: Best friend 1 and 2.)


### Best Friend #6 and #7 - Pipeline and Out GridView
These objects are kinda cool, and have a lot more properties than I would have guessed that a process has. Yay I'm learning!
Let's use our last Best Friend to view and sort ALL of the properties of an object: Out-GridView

```powershell
# Get all the process on the machine and display in an Grid View
Get-Process | Out-GridView

```
Finally back to a GUI! Play around with the filters and sorts. Kinda feels like an excel sheet right? (How do you think one would 'export' something to 'excel'?)

So what just happened? We retrieved an object and passed it on to the next command using the pipe character (usually between the Backspace and Enter Key). Cmdlets can be written to "catch" objects that are passed to them. out-gridview can catch any object and display all of it's properties (but not methods).

- What do you think would happen if you ran the following command?

```powershell
    Get-Process chrome | Stop-Process
```

## More Challenges:
Use PowerShell to answer the following:
- Get the status of the BITS service.
- What is 9354 multiplied by 8675309?
- Save a credential inside the variable $cred.
- Display the password in the clear.
- Test your connection to google.com on port 443
- Get your public IP by using the rest API at ipinfo.io