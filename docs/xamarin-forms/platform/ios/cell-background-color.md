---
title: Hintergrundfarbe der Zelle unter iOS
description: Plattformeigenschaften können Sie Funktionen zu nutzen, die nur auf einer bestimmten Plattform verfügbar ist ohne die Implementierung der benutzerdefinierten Renderern und Effekte. In diesem Artikel wird erläutert, wie die plattformspezifischen iOS nutzen, die die Standardhintergrundfarbe der Zellen für iOS festlegt wird.
ms.prod: xamarin
ms.assetid: 2A3FDACF-5AE2-40DE-8488-6FE41733712F
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/24/2018
ms.openlocfilehash: 396e674bb3e5642f7c54455ee9e30ba5bf232f18
ms.sourcegitcommit: 00744f754527e5b55154365f89691caaf1c9d929
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/07/2019
ms.locfileid: "57557412"
---
# <a name="cell-background-color-on-ios"></a>Hintergrundfarbe der Zelle unter iOS

[![Beispiel herunterladen](~/media/shared/download.png) Das Beispiel herunterladen](https://developer.xamarin.com/samples/xamarin-forms/userinterface/platformspecifics/)

Dieses iOS-Plattform-spezifische legt die Standardhintergrundfarbe der [ `Cell` ](xref:Xamarin.Forms.Cell) Instanzen. Es ist in XAML verwendet, durch Festlegen der `Cell.DefaultBackgroundColor` bindbare Eigenschaft eine [ `Color` ](xref:Xamarin.Forms.Color):

```xaml
<ContentPage ...
             xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core">
    <StackLayout Margin="20">
        <ListView ItemsSource="{Binding GroupedEmployees}"
                  IsGroupingEnabled="true">
            <ListView.GroupHeaderTemplate>
                <DataTemplate>
                    <ViewCell ios:Cell.DefaultBackgroundColor="Teal">
                        <Label Margin="10,10"
                               Text="{Binding Key}"
                               FontAttributes="Bold" />
                    </ViewCell>
                </DataTemplate>
            </ListView.GroupHeaderTemplate>
            ...
        </ListView>
    </StackLayout>
</ContentPage>
```

Alternativ können sie aus c# mithilfe der fluent-API verwendet werden:

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.iOSSpecific;
...

var viewCell = new ViewCell { View = ... };
viewCell.On<iOS>().SetDefaultBackgroundColor(Color.Teal);
```

Die `ListView.On<iOS>` Methode gibt an, dass diese plattformspezifischen nur unter iOS ausgeführt wird. Die `Cell.SetDefaultBackgroundColor` Methode in der [ `Xamarin.Forms.PlatformConfiguration.iOSSpecific` ](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific) -Namespace, legt die Hintergrundfarbe der Zelle mit einem angegebenen [ `Color` ](xref:Xamarin.Forms.Color). Darüber hinaus die `Cell.DefaultBackgroundColor` Methode kann zum Abrufen der aktuellen Hintergrundfarbe der Zelle verwendet werden.

Das Ergebnis ist, die Farbe des Hintergrunds in ein [ `Cell` ](xref:Xamarin.Forms.Cell) kann festgelegt werden, zu einem bestimmten [ `Color` ](xref:Xamarin.Forms.Color):

[![Screenshot der Gruppenkopfzellen Blaugrün unter iOS](cell-background-color-images/group-header-cell-color.png "ListView mit Blaugrün Gruppenkopfzellen")](cell-background-color-images/group-header-cell-color-large.png#lightbox "ListView mit Gruppenkopfzellen Blaugrün")

## <a name="related-links"></a>Verwandte Links

- [PlatformSpecifics (Beispiel)](https://developer.xamarin.com/samples/xamarin-forms/userinterface/platformspecifics/)
- [Erstellen von Plattformeigenschaften](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [iOSSpecific API](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)
