# azure_scaleset_script
## Create Virtual Machine


`set-variable -name "USERNAME" -value "Your_UserName"

Set-Variable -name "PASSWORD" -value "Password"

New-AzResourceGroup -Name Your_ResourceGroup_Name -Location EastUS2

az vm create --name VM_Name --resource-group Your_ResourceGroup_Name --image 'Win2016Datacenter' --size Standard_B1s --location EastUS2 --admin-username $USERNAME --admin-password $PASSWORD --zone 2`
