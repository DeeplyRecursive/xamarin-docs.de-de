---
title: MDocArchiveToMsxDocConverter.exe Rver nicht gefunden. BaseCommand.OnRequest
ms.topic: article
ms.prod: xamarin
ms.assetid: F5AC6AC4-0E7C-4746-A7CF-872F0E75AFF4
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/21/2017
ms.openlocfilehash: 1e49c270d5836379d60f50ec72960ddc83bfbba4
ms.sourcegitcommit: 73bd0c7e5f237f0a1be70a6c1384309bb26609d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
# <a name="mdocarchivetomsxdocconverterexe-not-found-rverbasecommandonrequest"></a>MDocArchiveToMsxDocConverter.exe Rver nicht gefunden. BaseCommand.OnRequest

> [!IMPORTANT]
> Dieses Problem wurde in den neuesten Versionen von Xamarin behoben. Allerdings tritt das Problem auf die neueste Version der Software, bitte der Datei eine [neuen Fehler](~/cross-platform/troubleshooting/questions/howto-file-bug.md) mit Ihrer vollständigen versionsverwaltung-Informationen "und" vollständig "Ausgabeprotokoll erstellen.


## <a name="error-message"></a>Fehlermeldung

Dieser Fehler kann auftreten, der *Mac Serverprotokoll* in Visual Studio:

```
Error: /Developer/MonoTouch/usr/share/doc/MonoTouch/MDocArchiveToMsxDocConverter.exe not found
 rver.BaseCommand.OnRequest (System.Net.HttpListenerContext context, System.Object commandRequestState) [0x00000] in <filename unknown>:0
  at Mtb.Server.Listener.OnRequest (System.Object state) [0x00000] in <filename unknown>:0
```

In dieser Nachricht vorliegen 2 separate Probleme:

1.  `Error: /Developer/MonoTouch/usr/share/doc/MonoTouch/MDocArchiveToMsxDocConverter.exe not found`

    Dieser Fehler harmlos, aber es ist ebenfalls irreführend sein. Es [verloren](https://bugzilla.xamarin.com/show_bug.cgi?id=21667) in einer zukünftigen Version.

2.  `rver.BaseCommand.OnRequest (System.Net.HttpListenerContext context …`

    Dieser Fehler ist das eigentliche Problem. Leider aufgrund von einem [Einschränkung](https://bugzilla.xamarin.com/show_bug.cgi?id=22080) ist dieser ausnahmestapelüberwachung *unvollständige*. Wenn Sie feststellen, eine unvollständige stapelüberwachung wie folgt in die Mac-Serverprotokoll dass, sehen Sie sich die `~/Library/Logs/Xamarin/MonoTouchVS/mtbserver.log` Datei auf dem Mac-Build-Host die vollständige stapelüberwachung gefunden.