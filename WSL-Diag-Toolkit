## WSL Installer Dianostics - Automatically find WSL configuration issues and repair.

#-------------------------------------#
#        #####--- WIP ---#####        #
#   WSL Diagnostic + Repair Toolkkit  #
#          v0.8b 04-25-2024           #
#                     --WhaleLinguini #
#-------------------------------------#

cls
##elevate to admin
Write-Host "********************************************"
Write-Host "#  Checking for Administrator Elevation    #"
Write-Host "********************************************"

Write-Host "Prompting user to elevate if needed."
Write-Host " "
Write-Host " "

Start-Sleep -Milliseconds 2000

# Get the ID and security principal of the current user account
 $myWindowsID=[System.Security.Principal.WindowsIdentity]::GetCurrent()
 $myWindowsPrincipal=new-object System.Security.Principal.WindowsPrincipal($myWindowsID)

 # Get the security principal for the Administrator role
 $adminRole=[System.Security.Principal.WindowsBuiltInRole]::Administrator

 # Check to see if we are currently running "as Administrator"
 if ($myWindowsPrincipal.IsInRole($adminRole))
    {
    # We are running "as Administrator" - so change the title and background color to indicate this
    $Host.UI.RawUI.WindowTitle = $myInvocation.MyCommand.Definition + "(Elevated)"
    $Host.UI.RawUI.BackgroundColor = "Black"
	$Host.UI.RawUI.ForegroundColor = "Green"
    clear-host
    }
 else
    {
    # We are not running "as Administrator" - so relaunch as administrator

    # Create a new process object that starts PowerShell
    $newProcess = new-object System.Diagnostics.ProcessStartInfo "PowerShell";

    # Specify the current script path and name as a parameter
    $newProcess.Arguments = $myInvocation.MyCommand.Definition;

    # Indicate that the process should be elevated
    $newProcess.Verb = "runas";

    # Start the new process
    [System.Diagnostics.Process]::Start($newProcess);

    # Exit from the current, unelevated, process
    exit
    }

 # WL self note your code that needs to be elevated here
 
 $factory_color = (Get-Host).UI.RawUI.ForegroundColor
 $factory_colorb = (Get-Host).UI.RawUI.BackgroundColor
 
 
# fuzzy kitten exit.
function fuzzy_kittens(){
	$factory_color = (Get-Host).UI.RawUI.ForegroundColor
    Write-Host ""
    Remove-Item -Path (Join-Path -Path $scriptDir -ChildPath ".\wsldiag.tmp") -ErrorAction SilentlyContinue
    pause
    exit
}


function softPuppy_Progess {
    param(
        [int]$totalSteps,
        [int]$animationSpeed = 300  # Adjust animation speed (milliseconds)
    )

    $progressBarWidth = 20  # Width of the progress bar

    # Loop through each step
    for ($step = 1; $step -le $totalSteps; $step++) {
        # Calculate the progress percentage
        $progress = [math]::Round(($step / $totalSteps) * 100)

        # Calculate the number of filled and empty slots in the progress bar
        $filledSlots = [math]::Round(($progressBarWidth * $progress) / 100)
        $emptySlots = $progressBarWidth - $filledSlots

        # Build the progress bar string
        $progressBar = "[" + "-" * $filledSlots + (" " * $emptySlots) + "] $progress%"

        # Output the progress bar
        Write-Host -NoNewline $progressBar

        # Sleep for the specified animation speed
        Start-Sleep -Milliseconds $animationSpeed

        # Move the cursor back to the beginning of the line
        Write-Host -NoNewline "`r"
    }
}



function colorKrayns($string) {
    if ($string.StartsWith("[+]")) {
        $trimmedString = $string.Substring(3)
		$Host.UI.RawUI.ForegroundColor = "White"
		$Host.UI.RawUI.BackgroundColor = "DarkGreen"
        Write-Host "[" -NoNewline
        Write-Host "+" -NoNewline
        Write-Host "]" -NoNewline
		$Host.UI.RawUI.ForegroundColor = $factory_color
		$Host.UI.RawUI.BackgroundColor = $factory_colorb
		Write-Host  $trimmedString 
	}
	
	if ($string.StartsWith("[-]")) {
        $trimmedString = $string.Substring(3)
        Write-Host "[" -NoNewline
        $Host.UI.RawUI.ForegroundColor = "White"
        Write-Host "-" -NoNewline
        $Host.UI.RawUI.ForegroundColor = $factory_color
        Write-Host "]" -NoNewline
		Write-Host  $trimmedString 
	}
	
	## raw out, set color back in main script.
	if ($string.StartsWith("[#]")) {
		Write-Host 
        $Host.UI.RawUI.ForegroundColor = "Cyan"
        Write-Host $string
	}
	
	    if ($string.StartsWith("[E]")) {
        $trimmedString = $string.Substring(3)
		$Host.UI.RawUI.ForegroundColor = "White"
		$Host.UI.RawUI.BackgroundColor = "Red"
        Write-Host "[" -NoNewline
        Write-Host "+" -NoNewline
        Write-Host "]" -NoNewline
		$Host.UI.RawUI.ForegroundColor = $factory_color
		$Host.UI.RawUI.BackgroundColor = $factory_colorb
		Write-Host  $trimmedString 
	}
			
    } else {
        #Write-Host $string
    }



function Write-HostD {
		param(
			[string]$Message
		)
		$Delay = 550
		colorKrayns($Message)
		Start-Sleep -Milliseconds $Delay
}

cls
Write-Host "################################################################################################"
Write-Host " "
Write-Host " "
Write-Host "		 _ _ _ _____ __       ____  _                     _   _        "
Start-Sleep -Milliseconds 100
Write-Host "		| | | |   __|  |     |    \|_| __ ___ ___ ___ ___| |_|_|___    "
Start-Sleep -Milliseconds 100
Write-Host "		| | | |__   |  |__   |  |  | ||. | . |   | . |_ -|  _| |  _|   "
Start-Sleep -Milliseconds 100
Write-Host "		|_____|_____|_____|  |____/|_|___|_  |_|_|___|___| | |_|___|   "
Start-Sleep -Milliseconds 100
Write-Host "		                                 |___|           |__|          "
Start-Sleep -Milliseconds 100
Write-Host "		                           _   "
Start-Sleep -Milliseconds 100
Write-Host "		                         _| |_ "
Start-Sleep -Milliseconds 100
Write-Host "		                        |_   _|"
Start-Sleep -Milliseconds 100
Write-Host "		                          |_|  "
Start-Sleep -Milliseconds 100
Write-Host "		    _____             _        _____         _ "
Start-Sleep -Milliseconds 100
Write-Host "		   | __  |___ ___  __|_|___   |_   _|___ ___| |"
Start-Sleep -Milliseconds 100
Write-Host "		   |    -| -_| . ||. | |  _|    | | | . | . | |"
Start-Sleep -Milliseconds 100
Write-Host "		   |__|__|___|  _|___|_|_|      |_| |___|___|_|"
Start-Sleep -Milliseconds 100
Write-Host "		             |_|                               "
Start-Sleep -Milliseconds 100
Write-Host ""
Write-Host "																										--Whale Linguini"
Write-Host ""
Write-Host ""
Write-Host ""
Write-Host "Checking under the bed for monsters (or loading) ..."
softPuppy_Progess -totalSteps 10
Write-Host " "
Write-Host "################################################################################################"
Write-Host " "

Write-Host " "


function pkg_install($pkg) {
    Write-HostD "[-] Installing $pkg"
    (dism.exe /online /enable-feature /featurename:$pkg /all /norestart)
    Write-HostD "[+] -PASS- $pkg Installed."
    Write-Host ""
    Write-Host "I got kinda lazy at this point, and didn't make this script loop back around if multiple packages were missing. So... re-run this script to keep checking until you get to the end."
    pause
    break
}

function checkState($pkg) {
    ## read line 6 and 7 and check if state is enabled. Line can change if reboot is pending.
    $raw_state1 = (Get-Content ".\wsldiag.tmp")[6]
    ## clean up extra spaces from string
    $raw_state1 = $raw_state1 -replace '(^\s+|\s+$)','' -replace '\s+',' '
    $raw_state2 = (Get-Content ".\wsldiag.tmp")[7]
    $raw_state2 = $raw_state2 -replace '(^\s+|\s+$)','' -replace '\s+',' '
    
    ## check to see if the word 'Enabled' is in either string or not.
    if ($raw_state1 -like "*Enabled*" -or $raw_state2 -like "*Enabled*") { 
        Write-HostD "[+] -PASS- Current $pkg State: [Enabled]"
    } else {
        if ($raw_state1 -notlike "*Enabled*" -or $raw_state2 -notlike "*Enabled*") { 
            Write-HostD "[E] -ERROR- $pkg State Error: $raw_state"
            Write-Host " "
            $inst = Read-Host "Install package $pkg now? [Y/N]"
            If ($inst -eq 'Y' -or $start -eq 'y') {
                pkg_install($pkg)
            } else {
				$Host.UI.RawUI.ForegroundColor = $factory_color
                Write-Host "[DEBUG] User entered N/n or something else."
                Write-Host "[DEBUG] Exiting... kthxbye."
                fuzzy_kittens
            }
            
        }
    }
}

function whaleStamp(){
Write-Host " "
Write-Host " "
Write-Host " ________ __           __         _____   __                     __         __ "
Write-Host "|  |  |  |  |--.---.-.|  |.-----.|     |_|__|.-----.-----.--.--.|__|.-----.|__|"
Write-Host "|  |  |  |     |  _  ||  ||  -__||       |  ||     |  _  |  |  ||  ||     ||  |"
Write-Host "|________|__|__|___._||__||_____||_______|__||__|__|___  |_____||__||__|__||__|"
Write-Host "                                                   |_____|                     "
	
}
## vars
$scriptDir = $PWD

## cleanup
Remove-Item -Path (Join-Path -Path $scriptDir -ChildPath ".\wsldiag.tmp") -ErrorAction SilentlyContinue

## allow user to cancel before running.
Write-Host "Note: No changes will be made without user input."
Write-Host " "
Write-Host " "
$start = Read-Host "Start diagnostics for WSL? [Y/N]"
Write-Host ""
        
If ($start -eq 'Y' -or $start -eq 'y') {
    Write-HostD "[-] Starting diagnostics ..."
} else {
	$Host.UI.RawUI.ForegroundColor = $factory_color
    Write-Host "[DEBUG] User entered N/n or something else."
    Write-Host "[DEBUG] Exiting... kthxbye."
    fuzzy_kittens
}

## check that app packages are installed.
Write-HostD "[-] Starting system checks ..."
Write-Host " "
Start-Sleep -Milliseconds 250

Write-HostD "[-] Checking installed packages ..."

$wsl = (Get-WindowsOptionalFeature -FeatureName Microsoft-Windows-Subsystem-Linux -Online | Out-File -FilePath .\wsldiag.tmp)
checkState "WSL"

$vmp = (Get-WindowsOptionalFeature -FeatureName VirtualMachinePlatform -Online | Out-File -FilePath .\wsldiag.tmp)
checkState "VirtualMachinePlatform"

$hv = (Get-WindowsOptionalFeature -FeatureName Microsoft-Hyper-V-All -Online | Out-File -FilePath .\wsldiag.tmp)
checkState "Microsoft-Hyper-V"

Write-HostD "[+] -PASS- Packages for WSL detected as installed and Enabled!"
write-host " "
Start-Sleep -Seconds 1.2

Write-HostD "[-] Checking BIOS for virtualization"

## check bios for virtualization
$bios = (Get-CimInstance win32_processor).VirtualizationFirmwareEnabled | Out-File -FilePath .\wsldiag.tmp
$filePath = Join-Path -Path $scriptDir -ChildPath "\wsldiag.tmp"

## had to do this goofy, for some reason the output wanted to be 1 char a line.
if (Test-Path $filePath) {
    try {
        $reader = [System.IO.StreamReader]::new($filePath)

        while ($reader.Peek() -ge 0) {
            $line = $reader.ReadLine()
            
            If ($line -like "*True*") {
                Write-HostD "[+] -PASS- BIOS Virtualization State: [Enabled]"
                write-host " "
                Start-Sleep -Milliseconds 350
            } else {
                if ($line -notlike "*True*") {
                    Write-HostD "[E] -ERROR- BIOS Virtualization not detected as enabled!"
                    Write-Host " "
					$Host.UI.RawUI.ForegroundColor = $factory_color
                    Write-HostD "Please reboot into computers BIOS and enable Virtualization. Afterwards Re-Run the script to continue diagnostics."
                    $reader.Close()
                    fuzzy_kittens
                }
            }                       
        }
        
        $reader.Close()
    } catch {
        Write-Host "Error reading the file: $_"
        fuzzy_kittens
    }
} else {
    Write-Host "File not found: $filePath"
    fuzzy_kittens
}

write-host " "
Start-Sleep -Milliseconds 100
    
Write-HostD "[-] Checking BCD for HyperVisorLaunch type ..."
$bcd = (bcdedit /enum | Out-File -FilePath .\wsldiag.tmp)

## lazy copy pasta whatever....

if (Test-Path $filePath) {
    try {
        $reader = [System.IO.StreamReader]::new($filePath)

        while ($reader.Peek() -ge 0) {
            $line = $reader.ReadLine()
            
            If ($line -like "*hypervisorlaunchtype*") {
                
                If ($line -like "*On*" -or $line -like "*auto*") {
                    Write-HostD "[+] -PASS- Hypervisor Launch Type Set: [On/Auto]"
                    write-host " "
                    
                } else {
                    if ($line -like "*Off*") {
                        Write-HostD "[E] -ERROR- Hypervisor Launch Type Set: [Off]!"
                        Write-Host " "
                        $reader.Close()
                        
                        $fix = Read-Host "Set Hypervisor Launch Type to 'Auto' now? [Y/N]"
                        If ($fix -eq 'Y' -or $fix -eq 'y') {
                            Write-HostD "[-] Changing Hypervisor Launch Type ..."
                            (bcdedit /set hypervisorlaunchtype auto)
                            Start-Sleep -Seconds 1
                            Write-HostD "[+] -PASS- Launch Type Set to 'Auto'"
                            Write-HostD "[-] Checking setting applied correctly ..."
                            Write-Host " "
                            Write-HostD "[#] ---------------		     Raw BCD 		   ------------------ [#]"
                            (bcdedit /enum)
							Write-HostD "[#] ---------------		     END Raw  		   ------------------ [#]"
							write-hostD " "
							$Host.UI.RawUI.ForegroundColor = $factory_color
                            Write-Host " "
                            
                            $check = Read-Host "Is 'Hypervisorlaunchtype' correctly set to 'Auto'? [Y/N]"
                            If ($check -eq 'Y' -or $check -eq 'y') {
                                Write-HostD "[+] -PASS- Hypervisor Launch Type set Correct."
                                write-host " "
                                $reader.Close()
                            } else {
                                If ($check -ne 'Y' -or $check -ne 'y') {
									$Host.UI.RawUI.ForegroundColor = $factory_color
                                    Write-Host "[E] -ERROR- Unknown error. Sorry."
                                    fuzzy_kittens
                                }
                            }
                        } else {
							$Host.UI.RawUI.ForegroundColor = $factory_color
                            Write-Host "[DEBUG] User entered N/n or something else."
                            Write-Host "[DEBUG] Exiting... kthxbye."
                            fuzzy_kittens
                        }
                    }
                }                
            }     
        }
        $reader.Close()
    } catch {
        Write-Host "Error reading the file: $_"
        pause
        exit
    }   
} else {
    Write-Host "File not found: $filePath"
    pause
    exit
}

Write-HostD "[-] Checking for vmcompute dlls ..."
write-host " "
Write-HostD "[#] ---------------		     Raw Out  		   ------------------ [#]"
Write-Host " "
(ls C:\Windows\System32\vmcompute*)
Write-Host " "
Write-HostD "[#] ---------------		     END Raw  		   ------------------ [#]"
Write-Host " "
$Host.UI.RawUI.ForegroundColor = $factory_color
Write-Host ""
Write-HostD "[-] Parsing VMCompute Service ..."

(Get-Service vmcompute | Out-File -FilePath .\wsldiag.tmp)

Start-Sleep -Milliseconds 300

$raw_state = (Get-Content ".\wsldiag.tmp")[3]
$raw_state = $raw_state -replace '(^\s+|\s+$)','' -replace '\s+',' '

if ($raw_state -like "*Running*") { 
        Write-HostD "[+] -PASS- VMCompute Service: [Running]"
        write-host " "
        Write-HostD "[+] -PASS- All System Checks Complete!"
        Write-Host ""
		$Host.UI.RawUI.ForegroundColor = "White"
		$Host.UI.RawUI.BackgroundColor = "DarkGreen"
		Write-Host ""
        Write-Host "Success! Script finished. Ideally, WSL should be working properly now. Please reboot if needed."
		Write-Host ""
		$Host.UI.RawUI.ForegroundColor = $factory_color
		$Host.UI.RawUI.BackgroundColor = $factory_colorb
		whaleStamp
        fuzzy_kittens
    } else {
        if ($raw_state -like "*Stopped*") { 
        Write-HostD "[E] -ERROR- VMCompute Service: [Stopped]"
        Write-Host ""
        $start = Read-Host "Attempt to start VMCompute Service now? [Y/N]"
            If ($start -eq 'Y' -or $start -eq 'y') {
                Write-HostD "[-] Starting VMCompute Service ..."
				Write-Host "----------------------------------------------------------------"
				Write-Host " "
                (net start VMCompute)
                Start-Sleep -Milliseconds 500
                (Get-Service vmcompute)
				Write-Host "----------------------------------------------------------------"
				Write-Host " "
                Start-Sleep -Second 1
                $check = Read-Host "Is VMCompute Service running now? [Y/N]"
					Write-Host " "
                    If ($start -eq 'Y' -or $start -eq 'y') {
                    Write-HostD "[+] -PASS- VMCompute Service Running."
                    write-host " "
                    Write-HostD "[+] -PASS- System Checks Complete!"
                    Write-Host ""
					$Host.UI.RawUI.ForegroundColor = "White"
					$Host.UI.RawUI.BackgroundColor = "DarkGreen"
					Write-Host ""
                    Write-Host "Success! Script finished. Ideally, WSL should be working properly now. Please reboot if needed."
					Write-Host ""
					$Host.UI.RawUI.ForegroundColor = $factory_color
					$Host.UI.RawUI.BackgroundColor = $factory_colorb
					whaleStamp
					fuzzy_kittens
                    } else {
                        If ($check -ne 'Y' -or $check -ne 'y') {
							$Host.UI.RawUI.ForegroundColor = $factory_color
                            Write-Host "[E] -ERROR- Error. Unknown error. Sorry."
                            fuzzy_kittens
                        }
                    }
            }
        }
    }

