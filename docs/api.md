
<br/><br/><br/>

<a id="createFeature"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  createFeature(name, [enabled], [publicFace], [appWillStart], [appDidStart], [extendedAspect]) ⇒ [`Feature`](#Feature)</h5>
Create a new Feature object, accumulating Aspect content to be


| Param | Type | Default | Description |
| --- | --- | --- | --- |
| name | string |  | the identity of the feature.  Feature names are used to index the [App Object](#app-object) by feature _(in support of [Cross Feature Communication](#cross-feature-communication))_, and are therefore guaranteed to be unique.  Application code can also use [Feature Name](#feature-name) in various [Single Source of Truth](#single-source-of-truth) operations. |
| [enabled] | boolean | <code>true</code> | an indicator as to whether this feature is enabled (true) or not (false).  When used, this indicator is typically based on a dynamic expression, allowing packaged code to be dynamically enabled/disabled at run-time _(please refer to: {{book.guide.enablement}})_. |
| [publicFace] | Any |  | an optional resource object that is the feature's Public API, promoting cross-communication between features.  This object is exposed through the App object as: `app.{featureName}.{publicFace}` _(please refer to: [publicFace and the App Object](#publicface-and-the-app-object))_. |
| [appWillStart] | [`appWillStartCB`](#appWillStartCB) |  | an optional [Application Life Cycle Hook](#application-life-cycle-hooks) invoked one time, just before the app starts up.  This life-cycle hook can do any type of initialization, and/or optionally supplement the app's top-level content (using a non-null return) _(please refer to: [appWillStart](#appwillstart))_. |
| [appDidStart] | [`appDidStartCB`](#appDidStartCB) |  | an optional [Application Life Cycle Hook](#application-life-cycle-hooks) invoked one time, immediately after the app has started.  Because the app is up-and-running at this time, you have access to the appState and the dispatch() function ... assuming you are using redux (when detected by feature-u's plugable aspects) _(please refer to: [appDidStart](#appdidstart))_. |
| [extendedAspect] | [`AspectContent`](#AspectContent) |  | additional aspects, as defined by the feature-u's pluggable Aspect extension. |

**Returns**: [`Feature`](#Feature) - a new Feature object (to be consumed by

<br/><br/><br/>

<a id="addBuiltInFeatureKeyword"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  addBuiltInFeatureKeyword(keyword)</h5>
Add additional Feature keyword (typically used by Aspect extensions


| Param | Type | Description |
| --- | --- | --- |
| keyword | string | the keyword name to add. |


<br/><br/><br/>

<a id="launchApp"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  launchApp([aspects], features, registerRootAppElm) ⇒ [`App`](#App)</h5>
Launch an app by assembling the supplied features, driving the


| Param | Type | Description |
| --- | --- | --- |
| [aspects] | [`Array.&lt;Aspect&gt;`](#Aspect) | the set of plugable aspects that extend feature-u, integrating other frameworks to match your specific run-time stack.  When NO aspects are supplied (an atypical case), only the very basic feature-u characteristics are in effect (like publicFace and life-cycle hooks). |
| features | [`Array.&lt;Feature&gt;`](#Feature) | the features that comprise this application. |
| registerRootAppElm | [`registerRootAppElmCB`](#registerRootAppElmCB) | the callback hook that registers the supplied root application element to the specific React framework used in the app.  Because this registration is accomplished by app-specific code, feature-u can operate in any of the react platforms, such as: React Web, React Native, Expo, etc. |

**Returns**: [`App`](#App) - the App object used to promote feature

<br/><br/><br/>

<a id="managedExpansion"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  managedExpansion(managedExpansionCB) ⇒ [`managedExpansionCB`](#managedExpansionCB)</h5>
Mark the supplied managedExpansionCB as a "managed expansion


| Param | Type | Description |
| --- | --- | --- |
| managedExpansionCB | [`managedExpansionCB`](#managedExpansionCB) | the callback function that when invoked (by feature-u) expands/returns the desired AspectContent. |

**Returns**: [`managedExpansionCB`](#managedExpansionCB) - the supplied managedExpansionCB,

<br/><br/><br/>

<a id="createAspect"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  createAspect(name, [validateConfiguration], [expandFeatureContent], validateFeatureContent, assembleFeatureContent, [assembleAspectResources], [injectRootAppElm], [additionalMethods]) ⇒ [`Aspect`](#Aspect)</h5>
Create an {{book.api.Aspect}} object, used to extend **feature-u**.


| Param | Type | Description |
| --- | --- | --- |
| name | string | the `Aspect.name` is used to "key" {{book.api.AspectContent}} of this type in the {{book.api.Feature}} object.<br/><br/> For example: an `Aspect.name: 'xyz'` would permit a `Feature.xyz: xyzContent` construct.<br/><br/> As a result, Aspect names cannot clash with built-in aspects, and they must be unique _(across all aspects that are in-use)_. |
| [validateConfiguration] | [`validateConfigurationMeth`](#validateConfigurationMeth) | an optional validation hook allowing this aspect to verify it's own required configuration (if any).<br/><br/> Some aspects may require certain settings in self for them to operate. |
| [expandFeatureContent] | [`expandFeatureContentMeth`](#expandFeatureContentMeth) | an optional aspect expansion hook, defaulting to the algorithm defined by {{book.api.managedExpansion}}.<br/><br/> This function rarely needs to be overridden.  It provides a hook to aspects that need to transfer additional content from the expansion function to the expanded content. |
| validateFeatureContent | [`validateFeatureContentMeth`](#validateFeatureContentMeth) | a validation hook allowing this aspect to verify it's content on the supplied feature (which is known to contain this aspect). |
| assembleFeatureContent | [`assembleFeatureContentMeth`](#assembleFeatureContentMeth) | the Aspect method that assembles content for this aspect across all features, retaining needed state for subsequent ops.<br/><br/> This method is required because this is the primary task that is accomplished by all aspects. |
| [assembleAspectResources] | [`assembleAspectResourcesMeth`](#assembleAspectResourcesMeth) | an optional Aspect method that assemble resources for this aspect across all other aspects, retaining needed state for subsequent ops.<br/><br/> This hook is executed after all the aspects have assembled their feature content (i.e. after {{book.api.assembleFeatureContentMeth}}). |
| [injectRootAppElm] | [`injectRootAppElmMeth`](#injectRootAppElmMeth) | an optional callback hook that promotes some characteristic of this aspect within the app root element (i.e. react component instance). |
| [additionalMethods] | Any | additional methods (proprietary to specific Aspects), supporting two different requirements:<br/><br/> 1. internal Aspect helper methods, and<br/><br/> 2. APIs used in "aspect cross-communication" ... a contract    between one or more aspects.  This is merely an API specified    by one Aspect, and used by another Aspect, that is facilitate    through the {{book.api.assembleAspectResourcesMeth$}}    hook. |

**Returns**: [`Aspect`](#Aspect) - a new Aspect object (to be consumed by {{book.api.launchApp}}).  

<br/><br/><br/>

<a id="Feature"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  Feature : Object</h5>
The Feature object is a container that holds


<br/><br/><br/>

<a id="appWillStartCB"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  appWillStartCB ⇒ reactElm</h5>
An optional app life-cycle hook invoked one time, just before the


| Param | Type | Description |
| --- | --- | --- |
| app | [`App`](#App) | the App object used in feature cross-communication. |
| curRootAppElm | reactElm | the current react app element root. |

**Returns**: reactElm - optionally, new top-level content (which in turn

<br/><br/><br/>

<a id="appDidStartCB"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  appDidStartCB : function</h5>
An optional app life-cycle hook invoked one time, immediately after


| Param | Type | Description |
| --- | --- | --- |
| app | [`App`](#App) | the App object used in feature cross-communication. |
| [appState] | Any | the redux top-level app state (when redux is in use). |
| [dispatch] | function | the redux dispatch() function (when redux is in use). |


<br/><br/><br/>

<a id="registerRootAppElmCB"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  registerRootAppElmCB : function</h5>
The launchApp() callback hook that registers the supplied root


| Param | Type | Description |
| --- | --- | --- |
| rootAppElm | reactElm | the root application element to be registered. |


<br/><br/><br/>

<a id="App"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  App : Object</h5>
The App object _(emitted from {{book.api.launchApp}})_ facilitates


<br/><br/><br/>

<a id="managedExpansionCB"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  managedExpansionCB ⇒ [`AspectContent`](#AspectContent)</h5>
A "managed expansion callback" (defined by


| Param | Type | Description |
| --- | --- | --- |
| app | [`App`](#App) | The feature-u app object, promoting the publicFace of each feature. |

**Returns**: [`AspectContent`](#AspectContent) - The desired AspectContent (ex: reducer,

<br/><br/><br/>

<a id="Aspect"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  Aspect : Object</h5>
Aspect objects (emitted from {{book.api.createAspect}}) are used to


<br/><br/><br/>

<a id="AspectContent"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  AspectContent : Any</h5>
The content (or payload) of an {{book.api.Aspect}}, specified


<br/><br/><br/>

<a id="validateConfigurationMeth"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  validateConfigurationMeth ⇒ string</h5>
A validation hook allowing this aspect to verify it's own required

**Returns**: string - an error message when self is in an invalid state

<br/><br/><br/>

<a id="expandFeatureContentMeth"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  expandFeatureContentMeth ⇒ string</h5>
Expand self's {{book.api.AspectContent}} in the supplied feature,


| Param | Type | Description |
| --- | --- | --- |
| app | [`App`](#App) | the App object used in feature cross-communication. |
| feature | [`Feature`](#Feature) | the feature which is known to contain this aspect **and** is in need of expansion (as defined by {{book.api.managedExpansion}}). |

**Returns**: string - an optional error message when the supplied

<br/><br/><br/>

<a id="validateFeatureContentMeth"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  validateFeatureContentMeth ⇒ string</h5>
A validation hook allowing this aspect to verify it's content on


| Param | Type | Description |
| --- | --- | --- |
| feature | [`Feature`](#Feature) | the feature to validate, which is known to contain this aspect. |

**Returns**: string - an error message string when the supplied feature

<br/><br/><br/>

<a id="assembleFeatureContentMeth"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  assembleFeatureContentMeth ⇒</h5>
The required Aspect method that assembles content for this aspect


| Param | Type | Description |
| --- | --- | --- |
| app | [`App`](#App) | the App object used in feature cross-communication. |
| activeFeatures | [`Array.&lt;Feature&gt;`](#Feature) | The set of active (enabled) features that comprise this application. |

**Returns**: void  

<br/><br/><br/>

<a id="assembleAspectResourcesMeth"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  assembleAspectResourcesMeth ⇒</h5>
An optional Aspect method that assemble resources for this aspect


| Param | Type | Description |
| --- | --- | --- |
| app | [`App`](#App) | the App object used in feature cross-communication. |
| aspects | [`Array.&lt;Aspect&gt;`](#Aspect) | The set of **feature-u** Aspect objects used in this this application. |

**Returns**: void  

<br/><br/><br/>

<a id="injectRootAppElmMeth"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  injectRootAppElmMeth ⇒ reactElm</h5>
An optional callback hook that promotes some characteristic of this


| Param | Type | Description |
| --- | --- | --- |
| app | [`App`](#App) | the App object used in feature cross-communication. |
| activeFeatures | [`Array.&lt;Feature&gt;`](#Feature) | The set of active (enabled) features that comprise this application.  This can be used in an optional Aspect/Feature cross-communication.  As an example, an Xyz Aspect may define a Feature API by which a Feature can inject DOM in conjunction with the Xyz Aspect DOM injection. |
| curRootAppElm | reactElm | the current react app element root. |

**Returns**: reactElm - a new react app element root (which in turn must