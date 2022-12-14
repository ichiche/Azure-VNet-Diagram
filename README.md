# Description

- The script is developed to export the VNet information in the format that recognized by **Diagrams.net**
- Virtual Network Diagram is actually generated by **Diagrams.net**
- Support up to 4 Tier Sequential vNet Peering
- 5 Types of Shapes of Virtual Network
    - With ExpressRoute Gateway and VPN Gateway coexist: Green
    - With ExpressRoute Gateway: Purple
    - With VPN Gateway: Blue
    - with Peering and without Gateway: Grey
    - Without Peering and Gateway: Red
- Exclude Databricks Virtual Network 
- [Optional] import the sample **diagrams_csv_sample.txt** to **Diagrams.net** for demonstration

# Instruction

1. Modify Global Parameter if necessary
1. Run the script to generate **Diagram CSV File**
1. Login **https://app.diagrams.net**
1. From the Web Console, click Arrange > Insert > Advanced > CSV
1. Remove all contents in CSV field
1. Copy and paste the content of **Diagram CSV File** in CSV field
1. Click Import
1. [Optional] Save as other format by Click File > Export as

# Baseline 

**The network flow diagram are generated in below preferred order, not enforced**

1. Virtual Network With ExpressRoute Gateway and VPN Gateway coexist
1. Virtual Network with ExpressRoute Gateway
1. Virtual Network with VPN Gateway
1. Highest Peering Count
1. Virtual Network Name in alphabetical order

# Constraints

- Partially automatic for generate the diagram
- Peering State is not shown
- Gateway Transit Status is not shown
- Associated ExpressRoute Circuit is not shown
- Subnet(s) of Virtual Network is not shown
- IP Addresses are not shown
- Subscription or Resource not found message could be ignore if the user account do not have access to all peered virtual network
- n-tier peering lookup is not supported yet 

# Sample

This is the diagram of the attached sample diagrams csv file, exported from **https://app.diagrams.net** as PNG format

<div>
    <img src="https://github.com/ichiche/Azure-VNet-Diagram/blob/main/diagrams_csv_sample.png" title="Diagram" alt="Diagram"
</div>

### Color

- Green (Both VPN and ER Gateway exist, with/without peer)
- Purple (ER Gateway exist, with/without peer)
- Blue (VPN Gateway exist, with/without peer)
- White (No Gateway, but peered to other VNet)
- Red (No Gateway and peer exist)

# Additional Information

Detail of Virtual Network and Peering are stored to below variable

```
$Global:vNet | Export-Csv -Path "C:\Temp\vNet-Detail.csv -NoTypeInformation -Confirm:$false -Force
$Global:vNetPeering | Export-Csv -Path "C:\Temp\vNetPeering-Detail.csv" -NoTypeInformation -Confirm:$false -Force
```
# Reference

- [Examples: Import from CSV to draw.io diagrams](https://drawio-app.com/import-from-csv-to-drawio)