---
title: 'Xamarin.Essentials: Problembehandlung'
description: In diesem Artikel wird beschrieben, wie Sie auftretende Fehler beim Entwickeln mit der Xamarin.Essentials-Bibliothek beheben.
ms.assetid: 2E474FAF-F841-4E3C-B815-F7ABD8EE3361
author: jamesmontemagno
ms.author: jamont
ms.date: 11/04/2018
ms.openlocfilehash: d13589680161de4c9b5d77eef6d5f823cc884136
ms.sourcegitcommit: 57e8a0a10246ff9a4bd37f01d67ddc635f81e723
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2019
ms.locfileid: "57671428"
---
# <a name="xamarinessentials-troubleshooting"></a>Xamarin.Essentials: Problembehandlung

## <a name="error-version-conflict-detected-for-xamarinandroidsupportcompat"></a>Fehler: Bei Xamarin.Android.Support.Compat wurde ein Versionskonflikt festgestellt.

Der folgende Fehler kann beim Aktualisieren von NuGet-Paketen (oder beim Hinzufügen eines neuen Pakets) mit einem Xamarin.Forms-Projekt auftreten, das Xamarin.Essentials verwendet:

```error
NU1107: Version conflict detected for Xamarin.Android.Support.Compat. Reference the package directly from the project to resolve this issue. 
 MyApp -> Xamarin.Essentials 0.8.0-preview -> Xamarin.Android.Support.CustomTabs 27.0.2.1 -> Xamarin.Android.Support.Compat (= 27.0.2.1) 
 MyApp -> Xamarin.Forms 3.1.0.583944 -> Xamarin.Android.Support.v4 25.4.0.2 -> Xamarin.Android.Support.Compat (= 25.4.0.2).
```

Das Problem liegt bei den nicht übereinstimmenden Abhängigkeiten der zwei NuGet-Pakete. Durch das Hinzufügen einer bestimmten Version der Abhängigkeit (in diesem Fall **Xamarin.Android.Support.Compat**), die beides unterstützt, kann das Problem behoben werden.

Fügen Sie dazu das NuGet-Paket, welches die Quelle des Konflikts darstellt, manuell hinzu, und verwenden Sie die **Versionsliste**, um eine bestimmte Version auszuwählen. Aktuell behebt die Version 27.0.2.1 der NuGet-Pakete Xamarin.Android.Support.Compat und Xamarin.Android.Support.Core.Util diesen Fehler.

Weitere Informationen finden Sie [in diesem Blogbeitrag](https://redth.codes/how-to-fix-the-dreaded-version-conflict-nuget-error-in-your-xamarin-android-projects/) und in einem Video zum Lösen des Problems.

Sollten bei Ihnen Probleme oder Fehler auftreten, melden Sie dies im [GitHub-Repository zu Xamarin.Essentials](https://github.com/xamarin/Essentials).
