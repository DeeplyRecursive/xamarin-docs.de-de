---
title: Erstellen eines ControlTemplate-Objekts
description: Steuerelementvorlagen können auf Anwendungsebene oder auf Seitenebene definiert werden. In diesem Artikel wird veranschaulicht, wie Sie Steuerelementvorlagen erstellen und verwenden.
ms.prod: xamarin
ms.assetid: A9AEB052-FBF5-4589-9BD4-6D6F62BED7F1
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 03/08/2016
ms.openlocfilehash: dc26084b94956ea9bc87384e5fdb79695bc8c2b5
ms.sourcegitcommit: be6f6a8f77679bb9675077ed25b5d2c753580b74
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2018
ms.locfileid: "53051781"
---
# <a name="creating-a-controltemplate"></a>Erstellen eines ControlTemplate-Objekts

[![Beispiel herunterladen](~/media/shared/download.png) Das Beispiel herunterladen](https://developer.xamarin.com/samples/xamarin-forms/templates/controltemplates/simpletheme/)

_Steuerelementvorlagen können auf Anwendungsebene oder auf Seitenebene definiert werden. In diesem Artikel wird veranschaulicht, wie Sie Steuerelementvorlagen erstellen und verwenden._

## <a name="creating-a-controltemplate-in-xaml"></a>Erstellen einer Steuerelementvorlage in XAML

Zum Definieren der [`ControlTemplate`](xref:Xamarin.Forms.ControlTemplate)-Klasse auf Anwendungsebene, müssen Sie der Klasse `App` ein [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary) hinzufügen. Standardmäßig verwenden alle Xamarin.Forms-Anwendungen, die aus einer Vorlage erstellt werden, die Klasse **App**. Damit wird die Unterklasse [`Application`](xref:Xamarin.Forms.Application) implementiert. Zum Deklarieren der `ControlTemplate`-Klasse auf Anwendungsebene muss bei `ResourceDictionary` in der Anwendung mithilfe von XAML die**App**-Standardklasse durch die XAML-**App**-Klasse und die dazugehörige CodeBehind-Datei ersetzt werden. Hier ein Codebeispiel:

```xaml
<Application xmlns="http://xamarin.com/schemas/2014/forms" xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" x:Class="SimpleTheme.App">
    <Application.Resources>
        <ResourceDictionary>
            <ControlTemplate x:Key="TealTemplate">
                <Grid>
                    ...
                    <BoxView ... />
                    <Label Text="Control Template Demo App"
                           TextColor="White"
                           VerticalOptions="Center" ... />
                    <ContentPresenter ... />
                    <BoxView Color="Teal" ... />
                    <Label Text="(c) Xamarin 2016"
                           TextColor="White"
                           VerticalOptions="Center" ... />
                </Grid>
            </ControlTemplate>
            <ControlTemplate x:Key="AquaTemplate">
                ...
            </ControlTemplate>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

Jede [`ControlTemplate`](xref:Xamarin.Forms.ControlTemplate)-Instanz wird als wiederverwendbares Objekt in einem [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary) erstellt.  Geben Sie dazu jeder Deklaration ein eindeutiges `x:Key`-Attribut, das sie mit einem aussagekräftigen Schlüssel im `ResourceDictionary` versieht.

Das folgende Codebeispiel zeigt das CodeBehind von `App`:

```csharp
public partial class App : Application
{
  public App ()
  {
    InitializeComponent ();
    MainPage = new HomePage ();
  }
}
```

Das CodeBehind muss sowohl die [`MainPage`](xref:Xamarin.Forms.Application.MainPage)-Eigenschaft festlegen als auch die `InitializeComponent`-Methode aufrufen, um die zugehörige XAML zu laden und zu analysieren.

Das folgende Codebeispiel zeigt eine [`ContentPage`](xref:Xamarin.Forms.ContentPage)-Klasse bei der ein `TealTemplate` auf [`ContentView`](xref:Xamarin.Forms.ContentView) angewendet wird:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms" xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" x:Class="SimpleTheme.HomePage">
    <ContentView x:Name="contentView" Padding="0,20,0,0"
                 ControlTemplate="{StaticResource TealTemplate}">
        <StackLayout VerticalOptions="CenterAndExpand">
            <Label Text="Welcome to the app!" HorizontalOptions="Center" />
            <Button Text="Change Theme" Clicked="OnButtonClicked" />
        </StackLayout>
    </ContentView>
</ContentPage>
```

Das `TealTemplate` wird der [`ContentView.ControlTemplate`](xref:Xamarin.Forms.TemplatedView.ControlTemplate)-Eigenschaft mithilfe der Markuperweiterung `StaticResource` zugewiesen. Die [`ContentView.Content`](xref:Xamarin.Forms.ContentView.Content)-Eigenschaft ist auf ein [`StackLayout`](xref:Xamarin.Forms.StackLayout) festgelegt. Damit wird der Inhalt für die [`ContentPage`](xref:Xamarin.Forms.ContentPage)-Klasse definiert. Dieser Inhalt wird mithilfe der [`ContentPresenter`](xref:Xamarin.Forms.ContentPresenter)-Klasse im `TealTemplate` angezeigt. Dies ergibt die in den folgenden Screenshots gezeigte Darstellung:

![](creating-images/teal-theme.png "Teal-Steuerelementvorlage")

### <a name="re-theming-an-application-at-runtime"></a>Ändern des Designs einer Anwendung zur Laufzeit

Mit einem Klick auf die Schaltfläche **Design ändern** wird die `OnButtonClicked`-Methode ausgeführt. Der dazugehörige Code sieht zum Beispiel so aus:

```csharp
void OnButtonClicked (object sender, EventArgs e)
{
  originalTemplate = !originalTemplate;
  contentView.ControlTemplate = (originalTemplate) ? tealTemplate : aquaTemplate;
}
```

Diese Methode ersetzt die aktive [`ControlTemplate`-](xref:Xamarin.Forms.ControlTemplate)-Instanz durch die alternative `ControlTemplate` Instanz. Dadurch ändert sich die Darstellung wie im folgenden Screenshot gezeigt:

![](creating-images/aqua-theme.png "Aqua-Steuerelementvorlage")

> [!NOTE]
> Für eine `ContentPage`-Klasse können Sie die Eigenschaft `Content` zuweisen und auch die Eigenschaft `ControlTemplate` festlegen. Wenn Sie das tun und die `ControlTemplate`-Instanz eine `ContentPresenter`-Instanz enthält, präsentiert `ContentPresenter` in `ControlTemplate` den Inhalt, der der `Content`-Eigenschaft zugewiesen ist.

### <a name="setting-a-controltemplate-with-a-style"></a>Festlegen von Steuerelementvorlagen mit einer Formatvorlagen

Sie können eine [`ControlTemplate`](xref:Xamarin.Forms.ControlTemplate)-Klasse auch mithilfe einer [`Style`](xref:Xamarin.Forms.Style)-Klasse anwenden, um die Designmöglichkeiten noch weiter zu erhöhen. Dazu erstellen Sie im [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary) eine *implizite* oder *explizite* Formatvorlage für die Zielansicht und legen in der [`Style`](xref:Xamarin.Forms.Style)-Instanz die `ControlTemplate`-Eigenschaft für die Zielansicht fest. Im folgenden Codebeispiel sehen Sie eine *implizite* Formatvorlage, die der Anwendungsebene [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary) hinzugefügt wurde:

```xaml
<Style TargetType="ContentView">
    <Setter Property="ControlTemplate" Value="{StaticResource TealTemplate}" />
</Style>
```

Da die [`Style`](xref:Xamarin.Forms.Style)-Instanz *implizit* ist, wird sie bei allen `ContentView`-Instanzen in der Anwendung verwendet. Daher ist es nicht mehr notwendig, die [`ContentView.ControlTemplate`](xref:Xamarin.Forms.TemplatedView.ControlTemplate) -Eigenschaft festzulegen. Folgendes Codebeispiel veranschaulicht dies:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms" xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" x:Class="SimpleTheme.HomePage">
    <ContentView x:Name="contentView" Padding="0,20,0,0">
      ...
    </ContentView>
</ContentPage>
```

Weitere Informationen zu Formatvorlagen finden Sie unter [Styles (Formatvorlagen)](~/xamarin-forms/user-interface/styles/index.md).

### <a name="creating-a-controltemplate-at-page-level"></a>Erstellen einer Steuerelementvorlage auf Seitenebene

Sie können [`ControlTemplate`](xref:Xamarin.Forms.ControlTemplate)-Instanzen nicht nur auf Anwendungsebene, sondern auch auf Seitenebene erstellen. Hier ein sehen Sie ein entsprechendes Codebeispiel:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms" xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" x:Class="SimpleTheme.HomePage">
    <ContentPage.Resources>
        <ResourceDictionary>
            <ControlTemplate x:Key="TealTemplate">
                ...
            </ControlTemplate>
            <ControlTemplate x:Key="AquaTemplate">
                ...
            </ControlTemplate>
        </ResourceDictionary>
    </ContentPage.Resources>
    <ContentView ... ControlTemplate="{StaticResource TealTemplate}">
        ...
    </ContentView>
</ContentPage>
```

Beim Hinzufügen einer [`ControlTemplate`](xref:Xamarin.Forms.ControlTemplate)-Klasse auf Seitenebene wird ein [`ResourceDictionary`](xref:Xamarin.Forms.ResourceDictionary) zur [`ContentPage`](xref:Xamarin.Forms.ContentPage)-Klasse hinzugefügt. Anschließend werden die `ControlTemplate`-Instanzen in das `ResourceDictionary` aufgenommen.

## <a name="creating-a-controltemplate-in-c35"></a>Erstellen einer Steuerelementvorlage in C&#35;

Zum Definieren einer [`ControlTemplate`](xref:Xamarin.Forms.ControlTemplate)-Klasse auf Anwendungsebene müssen Sie eine Klasse (`class`) erstellen, die die `ControlTemplate`-Klasse repräsentiert. Die Klasse sollte aus dem für die Vorlage verwendeten Layout ([layout](~/xamarin-forms/user-interface/layouts/index.md)) stammen, wie im folgenden Codebeispiel gezeigt:

```csharp
class TealTemplate : Grid
{
  public TealTemplate ()
  {
    ...
    var contentPresenter = new ContentPresenter ();
    Children.Add (contentPresenter, 0, 1);
    Grid.SetColumnSpan (contentPresenter, 2);
    ...
  }
}

class AquaTemplate : Grid
{
  ...
}
```

Die `AquaTemplate`-Klasse ist identisch mit der `TealTemplate`-Klasse, mit dem Unterschied, dass für die Eigenschaften [`BoxView.Color`](xref:Xamarin.Forms.BoxView.Color) und [`Label.TextColor`](xref:Xamarin.Forms.Label.TextColor) unterschiedliche Farben verwendet werden.

Das folgende Codebeispiel zeigt eine [`ContentPage`](xref:Xamarin.Forms.ContentPage)-Klasse bei der ein `TealTemplate` auf [`ContentView`](xref:Xamarin.Forms.ContentView) angewendet wird:

```csharp
public class HomePageCS : ContentPage
{
  ...
  ControlTemplate tealTemplate = new ControlTemplate (typeof(TealTemplate));
  ControlTemplate aquaTemplate = new ControlTemplate (typeof(AquaTemplate));

  public HomePageCS ()
  {
    var button = new Button { Text = "Change Theme" };
    var contentView = new ContentView {
      Padding = new Thickness (0, 20, 0, 0),
      Content = new StackLayout {
        VerticalOptions = LayoutOptions.CenterAndExpand,
        Children = {
          new Label { Text = "Welcome to the app!", HorizontalOptions = LayoutOptions.Center },
          button
        }
      },
      ControlTemplate = tealTemplate
    };
    ...
    Content = contentView;
  }
}
```

Sie erstellen die [`ControlTemplate`](xref:Xamarin.Forms.ControlTemplate)-Instanzen, indem Sie im `ControlTemplate`-Konstruktor den Typ der Klassen angeben, mit denen die Steuerelementvorlagen definiert werden.

Die [`ContentView.Content`](xref:Xamarin.Forms.ContentView.Content)-Eigenschaft ist auf ein [`StackLayout`](xref:Xamarin.Forms.StackLayout) festgelegt. Damit wird der Inhalt für die [`ContentPage`](xref:Xamarin.Forms.ContentPage)-Klasse definiert. Dieser Inhalt wird mithilfe der [`ContentPresenter`](xref:Xamarin.Forms.ContentPresenter)-Klasse im `TealTemplate` angezeigt. Nutzen Sie für den Wechsel zum Design `AquaTheme` während der Laufzeit die bereits vorher beschriebene Vorgehensweise.

## <a name="summary"></a>Zusammenfassung

In diesem Artikel haben Sie gelernt, wie Sie Steuerelementvorlagen erstellen und verwenden. Steuerelementvorlagen können auf Anwendungs- oder auf Seitenebene definiert werden.


## <a name="related-links"></a>Verwandte Links

- [Stile](~/xamarin-forms/user-interface/styles/index.md)
- [Simple Theme (Beispieldesign)](https://developer.xamarin.com/samples/xamarin-forms/templates/controltemplates/simpletheme/)
- [ControlTemplate](xref:Xamarin.Forms.ControlTemplate)
- [ContentPresenter](xref:Xamarin.Forms.ContentPresenter)
- [ContentView](xref:Xamarin.Forms.ContentView)
- [ResourceDictionary](xref:Xamarin.Forms.ResourceDictionary)
