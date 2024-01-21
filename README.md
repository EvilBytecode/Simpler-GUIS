PowerShell GUI Documentation
============================

# Syntax and Readability:
- Module saved me 10 lines of code!
- The Module approach uses custom functions like New-Label and New-Button, making the code more readable and concise.
- The raw PowerShell approach directly creates .NET objects, which may be less readable for those unfamiliar with the .NET framework.

# Abstraction:

- The Module abstracts away the details of control creation and layout management.
- The raw PowerShell approach requires more manual configuration of .NET objects for controls and layout.

# Modularity:

- The Module promotes modularity by encapsulating GUI-related functions in a separate module.
- The raw PowerShell approach involves creating controls directly in the script, potentially leading to less modular code.

# Ease of Use:

- The Module functions simplify the process of creating common UI elements, reducing the number of lines needed for the same functionality.
- The raw PowerShell approach involves more verbose syntax for creating controls and handling events.

## Module Code:
```powershell
Import-Module -Name 'C:\Users\comme\Downloads\GUIEasier\module\GUIHelper.psm1' -Force

$form = New-BasicForm -Title "PowerShell GUI Demo" -Width 400 -Height 200

$label = New-Label -Text "Enter your name:" -X 10 -Y 20
$txtbox = New-TextBox -Width 200 -Height 20 -X 150 -Y 20
$button = New-Button -Text "Submit" -X 10 -Y 10

$layout = Set-GridLayout -Control $form -RowCount 2 -ColumnCount 2
$layout.Controls.Add($label, 0, 0)
$layout.Controls.Add($txtbox, 0, 1)
$layout.Controls.Add($button, 1, 0)

$button.Add_Click({
        $name = $txtbox.Text
        Show-MessageBox -Message "Hello, $name!" -Title "Greeting"
    })

Show-GUI -Form $form
```

## Without Module:
```powershell
$form = New-Object System.Windows.Forms.Form
$form.Text = "PowerShell GUI Demo"
$form.Width = 400
$form.Height = 200

$label = New-Object System.Windows.Forms.Label
$label.Text = "Enter your name:"
$label.AutoSize = $true
$label.Location = New-Object System.Drawing.Point(10, 20)

$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Width = 200
$textBox.Height = 20
$textBox.Location = New-Object System.Drawing.Point(150, 20)

$button = New-Object System.Windows.Forms.Button
$button.Text = "Submit"
$button.Location = New-Object System.Drawing.Point(10, 60)

$button.Add_Click({
        $name = $textBox.Text
        [System.Windows.Forms.MessageBox]::Show("Hello, $name!", "Greeting")
    })

$form.Controls.Add($label)
$form.Controls.Add($textBox)
$form.Controls.Add($button)

[Windows.Markup.XamlLoader]::Load($form.ShowDialog())
```
