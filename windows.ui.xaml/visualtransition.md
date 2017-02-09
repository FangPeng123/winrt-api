---
-api-id: T:Windows.UI.Xaml.VisualTransition
-api-type: winrt class
---

<!-- Class syntax.
public class VisualTransition : Windows.UI.Xaml.DependencyObject, Windows.UI.Xaml.IVisualTransition
-->

# Windows.UI.Xaml.VisualTransition

## -description
Represents the visual behavior that occurs when the control transitions from one visual state to another.

## -xaml-syntax
```xaml

<VisualStateGroup>
  <!--one or more Visual State elements in the implicit States collection property -->
  <VisualStateGroup.Transitions>
    <VisualTransition>
      singleStoryboard
    </VisualTransition>
    <!--more transitions as above-->
  </VisualStateGroup.Transitions>
</VisualStateGroup>
```


## -remarks
A [VisualTransition](visualtransition.md) is a behavior that initiates a [Storyboard](visualtransition_storyboard.md). This [Storyboard](../windows.ui.xaml.media.animation/storyboard.md) is a timeline that declares the duration that animations that transition between two visual states will run. The transition can be defined differently for each combination of starting state (the **From** state) and ending state (the **To** state) as defined by your control's set of visual states. Transitions are defined by the [Transitions](visualstategroup_transitions.md) property of [VisualStateGroup](visualstategroup.md) and are usually defined in XAML. Most default control templates don't define transitions, and in this case the transitions between states happen instantaneously. The old state's modifications to the template are removed, and the new state's modifications are applied.

A [VisualTransition](visualtransition.md) references either one or two named visual states. The [From](visualtransition_from.md) value references the name of a state that is the current state. The [To](visualtransition_to.md) value references the name of a state that is the new state requested by a [GoToState](visualstatemanager_gotostate.md) call. These names come from an [x:Name attribute](http://msdn.microsoft.com/library/4ff1f3ed-903a-4305-b2bd-dcd29e0c9e6d) string value that is applied to a [VisualState](templatevisualstateattribute.md) as part of its definition in the same [VisualStateGroup](visualstategroup.md). Either [From](visualtransition_from.md) or [To](visualtransition_to.md) are a required value for an effective [VisualTransition](visualtransition.md), a [VisualTransition](visualtransition.md) that lacks either of these values or uses values that don't match existing states does nothing.

A [VisualTransition](visualtransition.md) can reference just a [From](visualtransition_from.md) state, just a [To](visualtransition_to.md) state, or both a [From](visualtransition_from.md) and [To](visualtransition_to.md) state. Omitting either [From](visualtransition_from.md) or [To](visualtransition_to.md) equates to any state. The [VisualStateManager](visualstatemanager.md) uses a precedence logic for which transition to apply whenever visual states change:
1. If a [VisualTransition](visualtransition.md) exists that specifically references the old state as [From](visualtransition_from.md) and the new state as [To](visualtransition_to.md), use that transition.
1. Otherwise, if a [VisualTransition](visualtransition.md) exists that specifically references the new state as [To](visualtransition_to.md) but does not specify [From](visualtransition_from.md), use that transition.
1. Finally, if a [VisualTransition](visualtransition.md) exists that specifically references the old state as [From](visualtransition_from.md) but does not specify [To](visualtransition_to.md), use that transition.
 If none of the above apply, no transition runs.

When you call [GoToState](visualstatemanager_gotostate.md) to change the visual state of a control, the [VisualStateManager](visualstatemanager.md) performs these actions:
+ If the [VisualState](visualstate.md) that the control was using prior to the newly requested visual state has a [Storyboard](visualstate_storyboard.md), that storyboard stops.
+ Between these actions, the [Storyboard](visualtransition_storyboard.md) for a [VisualTransition](visualtransition.md) runs, if a transition that involves the two visual states exists, and the named visual state requested by [GoToState](visualstatemanager_gotostate.md) is valid and is a new state.
+ If the [VisualState](visualstate.md) as named by *stateName* has a [Storyboard](visualstate_storyboard.md), the storyboard begins.


A [VisualTransition](visualtransition.md) can have a [Storyboard](visualstate_storyboard.md) value, a [GeneratedDuration](visualtransition_generatedduration.md) value or both. But if a [VisualTransition](visualtransition.md) has neither a [Storyboard](visualstate_storyboard.md) value nor a [GeneratedDuration](visualtransition_generatedduration.md) value, that [VisualTransition](visualtransition.md) does nothing in terms of animations, even if states named by the [From](visualtransition_from.md) and [To](visualtransition_to.md) values are involved in a state change.

### Implicit transitions

You can define a [VisualTransition](visualtransition.md) such that it has a [GeneratedDuration](visualtransition_generatedduration.md), but does not have any specific dependency properties being targeted and animated. This creates an implicit transition. Any dependency property that is specifically targeted for animation in either the [From](visualtransition_from.md) or[To](visualtransition_to.md) visual states and thus has different values across the state change then uses a generated transition animation. This generated animation transitions between the [From](visualtransition_from.md) state value and the [To](visualtransition_to.md) state value of such a property using interpolation. The implicit transition animation lasts for the time stated by [GeneratedDuration](visualtransition_generatedduration.md).

Implicit transitions only apply to properties that are a [Double](https://msdn.microsoft.com/library/system.double.aspx), [Color](../windows.ui/color.md) or [Point](../windows.foundation/point.md) value. In other words the property must be possible to implicitly animate using a [DoubleAnimation](../windows.ui.xaml.media.animation/doubleanimation.md), [PointAnimation](../windows.ui.xaml.media.animation/pointanimation.md) or [ColorAnimation](../windows.ui.xaml.media.animation/coloranimation.md). If you want to create a transition animation on some other value, for example a value that requires [ObjectAnimationUsingKeyFrames](../windows.ui.xaml.media.animation/objectanimationusingkeyframes.md), put that animation in the [Storyboard](visualstate_storyboard.md) and give the animation a [Duration](../windows.ui.xaml.media.animation/timeline_duration.md) that you want it to run.

By default, an implicit transition animation uses linear interpolation to animate a value through the [GeneratedDuration](visualtransition_generatedduration.md). You can change the linear interpolation to an interpolation behavior of your choice by setting [GeneratedEasingFunction](visualtransition_generatedeasingfunction.md) as well as [GeneratedDuration](visualtransition_generatedduration.md) on a [VisualTransition](visualtransition.md).

### Transition animations

There is another design pattern and API for displaying visual transitions for a Windows Store app using C++, C#, or Visual Basic. This concept is called *transition animations* and the class that implements the behavior is a *theme transition* or a *theme animation*. Rather than declaring transitions between visual states of the same control and applying changes to properties of control parts like you do with visual states, a transition animation represents changes in the relationship between a complete UI element and the overall app and UI. For example, there's a [RepositionThemeTransition](../windows.ui.xaml.media.animation/repositionthemetransition.md) that can be applied whenever a UI element is moved in the UI coordinate space of its layout container. Many of the transition animations are initiated by a user action. A transition animation applies to various **Transition** properties of [UIElement](uielement.md) and specific derived classes, not to a [VisualStateGroup](visualstategroup.md). Transition animations and theme animations are often built-in to the default behavior of a control. For more info, see [Storyboarded animations for visual states](http://msdn.microsoft.com/library/5e715281-d247-4e7f-9f88-2af0d88ed5e4).


<!--The following remark is relevant for Windows 8 > 8.1 migration. See WBB 465778-->
### Windows 8 behavior

For Windows 8, XAML theme transitions and various other automatic animated behaviors in the animation library didn't honor a particular Microsoft Windows  **Ease of Access** setting that enables users to turn off "unnecessary animations".

Starting with Windows 8.1, theme transitions, theme animations, and visual transitions all honor the **Turn off all unnecessary animations (when possible)** setting in **Ease of Access**. The animations won't run and the control state changes or visual changes are instantaneous.

If you migrate your app code from Windows 8 to Windows 8.1, you might want to test your animation behaviors with **Turn off all unnecessary animations (when possible)** setting enabled. Because some of these animations are controlled by storyboards, and because you sometimes chain up custom animations to start after visual transitions or theme animations are complete, the **Turn off all unnecessary animations (when possible)** setting might affect the timings of your animations. Also, if you've implemented something as a [VisualTransition](visualtransition.md) in a visual state rather than as a storyboarded animation, you might want to switch it to be a true custom animation, so that the **Turn off all unnecessary animations (when possible)** setting won't disable it.

Apps that were compiled for Windows 8 but running on Windows 8.1 continue to use the Windows 8 behavior for theme animations and visual transitions. However, theme transitions are disabled by the setting on Windows 8.1, even if an app is not recompiled.

## -examples
This example creates a [VisualTransition](visualtransition.md) that specifies that when the user moves the mouse away from the control, the control's border changes to blue, then to yellow, then to black in 1.5 seconds.



[!code-xml[8](../windows.ui.xaml.data/code/StylingTemplatingOverview/csharp/SkinnedButton.xaml#Snippet8)]



[!code-xml[VisualTransitions](../windows.ui.xaml.data/code/StylingTemplatingOverview/csharp/ButtonStages.xaml#SnippetVisualTransitions)]

## -see-also
[DependencyObject](dependencyobject.md), [Transitions](uielement_transitions.md), [VisualStateGroup](visualstategroup.md), [VisualStateManager](visualstatemanager.md), [Quickstart: Control templates](http://msdn.microsoft.com/library/67c424ae-afb1-4560-a6a8-4a3506775d77), [Storyboarded animations](http://msdn.microsoft.com/library/0cbceea0-2b0e-44a1-a09a-f7a939632f3a), [Storyboarded animations for visual states](http://msdn.microsoft.com/library/5e715281-d247-4e7f-9f88-2af0d88ed5e4)
, [Transitions](uielement_transitions.md), [VisualStateGroup](visualstategroup.md), [VisualStateManager](visualstatemanager.md), [Quickstart: Control templates](http://msdn.microsoft.com/library/67c424ae-afb1-4560-a6a8-4a3506775d77), [Storyboarded animations](http://msdn.microsoft.com/library/0cbceea0-2b0e-44a1-a09a-f7a939632f3a), [Storyboarded animations for visual states](http://msdn.microsoft.com/library/5e715281-d247-4e7f-9f88-2af0d88ed5e4)