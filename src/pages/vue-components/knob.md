---
title: Knob
desc: The QKnob Vue component is used to take a number input through mouse or touch panning.
keys: QKnob
related:
  - /vue-components/circular-progress
---

The QKnob component is used to take a number input from the user through mouse/touch panning. It is based on [QCircularProgress](/vue-components/circular-progress) and inherits all its properties and behavior.

## QKnob API

<doc-api file="QKnob" />

## 用法

By default, QKnob inherits current text color (as arc progress color and inner label color) and current font size (as component size). For customization, you can use the size and color related props.

### Basic 基础

<doc-example title="Basic" file="QKnob/Basic" />

### Show value

In the example below, `show-value` property also enables the default slot, so you can fill it with custom content, like even a QAvatar or a QTooltip. The `font-size` prop refers to the inner label font size.

<doc-example title="Show value" file="QKnob/ShowValue" />

### Min and max

<doc-example title="Custom min/max" file="QKnob/MinMax" />

### Inner min/max <q-badge align="top" color="brand-primary" label="v2.5.4+" />

Sometimes you need to restrict the model value to an interval inside of the track's length. For this purpose, use `inner-min` and `inner-max` props. First prop needs to be higher or equal to `min` prop while the latter needs to be lower or equal to the `max` prop.

<doc-example title="Inner min/max" file="QKnob/InnerMinMax" />

### Custom step

<doc-example title="Custom step" file="QKnob/Step" />

### Offset angle

<doc-example title="Offset angle" file="QKnob/Angle" />

### Disable and readonly

<doc-example title="Disable and readonly" file="QKnob/DisableReadonly" />

### Native form submit

When dealing with a native form which has an `action` and a `method` (eg. when using Quasar with ASP.NET controllers), you need to specify the `name` property on QKnob, otherwise formData will not contain it (if it should):

<doc-example title="Native form" file="QKnob/NativeForm" />
