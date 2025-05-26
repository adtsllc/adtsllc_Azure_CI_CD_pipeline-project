# adtsllc_Azure_CI_CD_pipeline-project
# Project user guide and documentation in Azure Cloud.
  git checkout -b dev-001-azure # to create a new branch"
  vi pipeline.yml "Create a file and input the content"
  git status
  git add .
  git commit -am "pipeline commit"
  git push
  git push --set-upstream origin dev-001-azure


  Get Azure VPN Gateway Public IP: You'll need this to configure your on-premises VPN device.

ARM: Look at the outputs of the deployment if you add output sections to the template.

CLI: az network vpn-gateway show --resource-group $RESOURCE_GROUP --name $VPN_GATEWAY_NAME --query "ipConfigurations[0].publicIpAddress.ipAddress" -o tsv

PowerShell: $vpnGateway = Get-AzVpnGateway -ResourceGroupName $resourceGroupName -Name $vpnGatewayName; $vpnGateway.BgpSettings.VpnGatewayIpAddresses[0] (If BGP is enabled) or you might need to inspect the connection properties or associated public IP resource. For non-BGP, it's typically shown in the portal or via Get-AzPublicIpAddress.
Configure On-Premises VPN Device: Use the Azure VPN Gateway's public IP, the pre-shared key, and the relevant IPsec/IKE parameters (usually IKEv2, AES256, SHA256, DH Group 14/24 or higher for Phase 1 & 2) to configure your on-premises VPN device. Ensure local and remote network address spaces are correctly defined on both sides.

Verify Connectivity: Once both sides are configured, the VPN tunnel should establish. You can monitor the connection status in the Azure portal under your VWAN Hub's VPN Gateway connections.
