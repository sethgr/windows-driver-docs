---
title: MS\_SMHBA\_SCSIENTRY WMI Class
description: MS\_SMHBA\_SCSIENTRY WMI Class
ms.assetid: 8ac7a979-b3fe-4da6-a8e7-301c64b27e46
ms.localizationpriority: medium
ms.date: 10/17/2018
---

# MS\_SMHBA\_SCSIENTRY WMI Class


An HBA miniport driver that supports the Storage Management API uses the MS\_SMHBA\_SCSIENTRY class to store information that is generated by the operating system that uniquely identifies a SCSI logical unit and its adapter. This class is used to construct a binding between the operating system information and the SSP identifier for the logical unit.

The MS\_SMHBA\_SCSIENTRY class is defined as follows in *Hbaapi.mof*:

```cpp
class MS_SMHBA_SCSIENTRY
{
    [HBAType("MS_SMHBA_PORTLUN"), WmiDataId(1)]
    MS_SMHBA_PORTLUN PortLun;

    [HBAType("HBA_LUID"), WmiDataId(2)]
    uint8  LUID[256];

    [HBAType("HBA_SCSIID"), WmiDataId(3)]
    HBAScsiID ScsiId;
};
```

When this class definition is compiled by the WMI tool suite, it produces the following data structure:

[**MS\_SMHBA\_SCSIENTRY**](https://msdn.microsoft.com/library/windows/hardware/ff563191)

There are no methods associated with this WMI class.

 

 




