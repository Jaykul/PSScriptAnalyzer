# AvoidDefaultValueForMandatoryParameter

**Severity Level: Warning**

## Description

Most mandatory parameters should not have default values, because the default value can only be used if there is an additional parameter set where the parameter _is not_ mandatory. When a parameter _is_ mandatory, PowerShell prompts for a value unless a value is provided in the call to the function, so the default value is ignored. 

Note: this rule does not currently check for multiple parameter sets. If this parameter is only mandatory in some parameter sets, you _may_ provide a default value, but should take care when doing so. It can be confusing to maintainers, and you must be careful to only use parameters to calculate the value if they are set in the parameter set(s). In that case, you'll need to suppress this message -- see https://github.com/PowerShell/PSScriptAnalyzer/blob/master/README.md#suppressing-rules

## Example

### Wrong

```powershell
function Test
{

    [CmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$true)]
        $Parameter1 = 'default Value'
    )
}
```

### Correct

```powershell
function Test
{
    [CmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$true)]
        $Parameter1
    )
}
```
