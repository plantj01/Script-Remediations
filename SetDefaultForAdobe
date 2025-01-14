# Remco Daemen 16-11-2024
#
# As browsers keep trying to set themselves as defaultprogram to open PDF files, it was required to reset the defaultprogram for PDF. 
# As there were different versions of Adobe (Reader & Pro) i had to make a custom script for this. 
# The script checks if Pro is installed, then sets the required program as default. 

# Check if Adobe Acrobat Pro is installed
$acrobatProInstalled = Test-Path "C:\Program Files (x86)\Adobe\Acrobat DC\Acrobat\Acrobat.exe"

# Define file extensions and corresponding ProgIDs
$extensions = @('.pdf', '.pdx')
if ($acrobatProInstalled) {
    $progID = "{91F10FCC-6C89-4F7D-917B-15022B7541CD}"  # Use the specified ProgID for Adobe Acrobat Pro
} else {
    $progID = "{AC76BA86-1033-1033-7760-BC15014EA700}"  # Replace with the correct ProgID for your version of Adobe Reader
}

# Set file associations for each extension
foreach ($extension in $extensions) {
    $fileType = Get-ItemProperty -Path "HKCU:\Software\Classes\$extension"
    if ($fileType.PSChildName -eq $null) {
        New-Item -Path "HKCU:\Software\Classes\$extension" -Force
    }

    Set-ItemProperty -Path "HKCU:\Software\Classes\$extension" -Name "(Default)" -Value $progID
}
