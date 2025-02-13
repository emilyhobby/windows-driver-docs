---
title: so (Set Kernel Debugging Options)
description: The so command sets or displays the kernel debugging options.
keywords: ["so (Set Kernel Debugging Options) Windows Debugging"]
ms.date: 05/23/2017
topic_type:
- apiref
ms.topic: reference
api_name:
- so (Set Kernel Debugging Options)
api_type:
- NA
---

# so (Set Kernel Debugging Options)


The **so** command sets or displays the kernel debugging options.

```dbgcmd
so [Options] 
```

## <span id="ddk_cmd_set_kernel_debugging_options_dbg"></span><span id="DDK_CMD_SET_KERNEL_DEBUGGING_OPTIONS_DBG"></span>Parameters


*Options*
One or more of the following options:

<span id="NOEXTWARNING"></span><span id="noextwarning"></span>**NOEXTWARNING**  
Does not issue a warning when the debugger cannot find an extension command.

<span id="NOVERSIONCHECK"></span><span id="noversioncheck"></span>**NOVERSIONCHECK**  
Does not check the version of debugger extension DLLs.

If you omit *Options*, the current options are displayed.

### Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>Kernel mode only</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Targets</strong></p></td>
<td align="left"><p>Live, crash dump</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>All</p></td>
</tr>
</tbody>
</table>

 

## Remarks

You can also set kernel debugging options using the \_NT\_DEBUG\_OPTIONS [environment variable](kernel-mode-environment-variables.md).

 

 





