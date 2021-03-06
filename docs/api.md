
<br/><br/><br/>

<a id="assertNoRootAppElm"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  assertNoRootAppElm(rootAppElm, className)</h5>
A convenience function that asserts the supplied `rootAppElm` is NOTdefined.When this constraint is not met, and error is thrown, afteremitting applicable context in the console log.For more information, please refer to{{book.guide.injectingDomContent}}.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>rootAppElm</td><td>reactElm</td><td><p>the current react app element root to
check.</p>
</td>
    </tr><tr>
    <td>className</td><td>string</td><td><p>the className on behalf of which this
assertion is performed.</p>
</td>
    </tr>  </tbody>
</table>


<br/><br/><br/>

<a id="createFeature"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  createFeature(name, [enabled], [fassets], [appWillStart], [appInit], [appDidStart], [extendedAspect]) ⇒ [`Feature`](#Feature)</h5>
Create a new {{book.api.Feature}} object, cataloging{{book.api.AspectContent}} to be consumed by{{book.api.launchApp}}.  Each feature within an applicationpromotes it's own {{book.api.Feature}} object.For more information, please refer to{{book.guide.detail_featureAndAspect}}.**Please Note** this function uses named parameters.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Default</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>name</td><td>string</td><td></td><td><p>the identity of the feature.  Feature names
are guaranteed to be unique.  Application code can use the Feature
name in various <strong>single-source-of-truth</strong> operations <em>(see
{{book.guide.bestPractices}})</em>.</p>
</td>
    </tr><tr>
    <td>[enabled]</td><td>boolean</td><td><code>true</code></td><td><p>an indicator as to whether this
feature is enabled (true) or not (false).  When used, this
indicator is typically based on a dynamic expression, allowing
packaged code to be dynamically enabled/disabled at run-time
<em>(please refer to: {{book.guide.enablement}})</em>.</p>
</td>
    </tr><tr>
    <td>[fassets]</td><td><a href="#fassets"><code>fassets</code></a></td><td></td><td><p>an optional aspect that promotes feature assets used in
{{book.guide.crossCom}} (i.e. the Public Face of a feature).
<code>fassets</code> directives can both define resources, and/or declare a
resource contract (the intention to use a set of fasset resources).
Resources are accumulated across all features, and exposed through
the {{book.api.FassetsObject}}, and the {{book.api.withFassets}}
HoC.</p>
</td>
    </tr><tr>
    <td>[appWillStart]</td><td><a href="#appWillStartCB"><code>appWillStartCB</code></a></td><td></td><td><p>an optional
{{book.guide.appLifeCycle}} invoked one time, just before the app
starts up.  This life-cycle hook can do any type of initialization,
and/or optionally supplement the app&#39;s top-level content (using a
non-null return) <em>(please refer to: {{book.guide.appWillStart}})</em>.</p>
</td>
    </tr><tr>
    <td>[appInit]</td><td><a href="#appInitCB"><code>appInitCB</code></a></td><td></td><td><p>an optional
{{book.guide.appLifeCycle}} invoked one time, later in the app
startup process.  This life-cycle hook supports blocking async
initialization (by simply returning a promise) <em>(please refer to:
{{book.guide.appInit}})</em>.</p>
</td>
    </tr><tr>
    <td>[appDidStart]</td><td><a href="#appDidStartCB"><code>appDidStartCB</code></a></td><td></td><td><p>an optional
{{book.guide.appLifeCycle}} invoked one time, immediately after the
app has started <em>(please refer to: {{book.guide.appDidStart}})</em>.</p>
</td>
    </tr><tr>
    <td>[extendedAspect]</td><td><a href="#AspectContent"><code>AspectContent</code></a></td><td></td><td><p>additional aspects, as
defined by the feature-u&#39;s Aspect plugins (please refer to:
{{book.guide.detail_extendableAspects}} -and-
{{book.guide.extending}}).</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: [`Feature`](#Feature) - a new Feature object (to be consumed bylaunchApp()).  

<br/><br/><br/>

<a id="extendFeatureProperty"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  extendFeatureProperty(name, owner)</h5>
Extend valid Feature properties to include the supplied name... used when extending APIs for{{book.guide.extending_aspectCrossCommunication}}.**feature-u** keeps track of the agent that owns this extension(using the owner parameter).  This is used to prevent exceptionswhen duplicate extension requests are made by the same owner.  Thiscan happen when multiple instances of an aspect type are supported,and also in unit testing.

**Throws**:

- Error when supplied name is already reserved by a different owner

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>name</td><td>string</td><td><p>the property name to allow.</p>
</td>
    </tr><tr>
    <td>owner</td><td>string</td><td><p>the requesting owner id of this extension
request.  Use any string that uniquely identifies your utility
<em>(such as the aspect&#39;s npm package name)</em>.</p>
</td>
    </tr>  </tbody>
</table>


<br/><br/><br/>

<a id="expandWithFassets"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  expandWithFassets(expandWithFassetsCB) ⇒ [`expandWithFassetsCB`](#expandWithFassetsCB)</h5>
Mark the supplied {{book.api.expandWithFassetsCB}} as a "ManagedExpansion Callback", distinguishing it from other functions _(suchas reducer functions)_.Features may communicate {{book.api.AspectContent}} directly, orthrough a {{book.api.expandWithFassetsCB}}.  In other words, the{{book.api.AspectContent}} can either be the actual content itself_(ex: reducer, logic modules, etc.)_, or a function that returnsthe content.  The latter: 1. supports {{book.guide.crossCom}} _(through fassets object    injection)_, and 2. minimizes circular dependency issues (of ES6 modules).Managed Expansion Callbacks are used when a fully resolved{{book.api.FassetsObject}} is required during in-line code expansion.They are merely functions that when invoked _(under the control of**feature-u**)_, are supplied the {{book.api.FassetsObject}} andreturn the expanded {{book.api.AspectContent}} _(ex: reducer, logicmodules, etc.)_.**For more information _(with examples)_**, please refer to{{book.guide.crossCom_managedCodeExpansion}}.The {{book.api.expandWithFassetsCB}} function should conform to thefollowing signature:**API:** {{book.api.expandWithFassetsCB$}}

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>expandWithFassetsCB</td><td><a href="#expandWithFassetsCB"><code>expandWithFassetsCB</code></a></td><td><p>the callback
function that when invoked (by <strong>feature-u</strong>) expands/returns the
desired {{book.api.AspectContent}}.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: [`expandWithFassetsCB`](#expandWithFassetsCB) - the supplied expandWithFassetsCB,marked as a "managed expansion callback".  

<br/><br/><br/>

<a id="launchApp"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  launchApp(features, [aspects], registerRootAppElm, [showStatus]) ⇒ [`Fassets`](#Fassets)</h5>
Launch an application by assembling the supplied features, drivingthe configuration of the frameworks in use _(as orchestrated by thesupplied set of plugable Aspects)_.For more information _(with examples)_, please refer to{{book.guide.detail_launchingApp}}.**Please Note** this function uses named parameters.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>features</td><td><a href="#Feature"><code>Array.&lt;Feature&gt;</code></a></td><td><p>the features that comprise this
application.</p>
</td>
    </tr><tr>
    <td>[aspects]</td><td><a href="#Aspect"><code>Array.&lt;Aspect&gt;</code></a></td><td><p>the set of plugable Aspects that extend
<strong>feature-u</strong>, integrating other frameworks to match your specific
run-time stack.<br/><br/></p>
<p>When NO Aspects are supplied <em>(an atypical case)</em>, only the very
basic <strong>feature-u</strong> characteristics are in effect (like fassets
and life-cycle hooks).</p>
</td>
    </tr><tr>
    <td>registerRootAppElm</td><td><a href="#registerRootAppElmCB"><code>registerRootAppElmCB</code></a></td><td><p>the callback hook
that registers the supplied root application element to the specific
React framework used in the app.<br/><br/></p>
<p>Because this registration is accomplished by app-specific code,
<strong>feature-u</strong> can operate in any of the react platforms, such as:
{{book.ext.react}} web, {{book.ext.reactNative}},
{{book.ext.expo}}, etc.<br/><br/></p>
<p>Please refer to {{book.guide.detail_reactRegistration}} for more
details and complete examples.</p>
</td>
    </tr><tr>
    <td>[showStatus]</td><td><a href="#showStatusCB"><code>showStatusCB</code></a></td><td><p>an optional callback hook that
communicates a blocking &quot;persistent&quot; status message to the end
user.</p>
<p>Please refer to {{book.api.showStatusCB}} for more information.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: [`Fassets`](#Fassets) - the Fassets object used in cross-feature-communication.  

<br/><br/><br/>

<a id="useFassets"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  useFassets(p) ⇒ [`Fassets`](#Fassets) \| fassets-resource \| fassetsProps</h5>
A {{book.ext.reactHook}} that provides functional component accessto **feature-u** {{book.api.fassets}}.**Hooks** allow you to **"hook into"** React state and lifecycleaspects _from functional components_.  They greatly simplify the UIimplementation _as opposed to the alternative of Higher OrderComponents (see: {{book.api.withFassets}})_.There are three ways to invoke `useFassets()` _(examples can befound at {{book.guide.crossCom_uiComposition}})_:1. Passing NO parameters, returns the   {{book.api.FassetsObject}}:   ```js   + useFassets(): fassets   ```2. Passing a `fassetsKey` _(a string)_, returns the resolved   fassets resource:   ```js   + useFassets('MainPage.*.link@withKeys'): [] ... an array of cataloged links   ```   The `fassetsKey` parameter is identical _(in usage)_ to the   {{book.api.Fassets_get}} method.3. Passing a {{book.api.mapFassetsToPropsStruct}}, returns a set of   resolved fassetsProps:   ```js   + useFassets({       mainBodies: 'MainPage.*.body',       mainLinks:  'MainPage.*.link@withKeys'     }): {  // ... return structure:       mainBodies: ... resolved cataloged resource       mainLinks:  ... ditto     }   ```   The {{book.api.mapFassetsToPropsStruct}} allows you to return   more than one resolved fassets resources.**SideBar**: For `useFassets()` to operate,`<FassetsContext.Provider>` must be rendered at the root of yourapplication DOM.  This is really a moot point, because**feature-u** automatically performs this initialization, so youreally don't have to worry about this detail _(automatingconfiguration is a Hallmark of **feature-u** - reducing boilerplatecode)_.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>p</td><td>string | <a href="#mapFassetsToPropsStruct"><code>mapFassetsToPropsStruct</code></a></td><td><p>the parameter controlling
what <code>useFassets</code> does <em>(see explanation above)</em>.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: [`Fassets`](#Fassets) \| fassets-resource \| fassetsProps - _see explanation above_.  

<br/><br/><br/>

<a id="withFassets"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  withFassets(mapFassetsToProps, [component]) ⇒ HoC \| HoF</h5>
Promotes a "wrapped" Component (an HoC - Higher-order Component)that injects fasset props into a `component`, as specified by the`mapFassetsToProps` parameter.  Please refer to the{{book.api.mapFassetsToPropsStruct}} for the details of what thismapping construct looks like. Examples can be found at{{book.guide.crossCom_uiComposition}}.Central to this process, a Higher-order Function (HoF) is createdthat encapsulates this "mapping knowledge".  Ultimately, thisHoF must be invoked (passing `component`), which exposes the HoC(the "wrapped" Component).```js+ withFassetsHoF(component): HoC```There are two ways to use `withFassets()`:1. By directly passing the `component` parameter, the HoC will be   returned _(internally invoking the HoF)_.  This is the most   common use case.2. By omitting the `component` parameter, the HoF will be   returned.  This is useful to facilitate "functional composition"   _(in functional programming)_.  In this case it is the client's   responsibility to invoke the HoF _(either directly or   indirectly)_ in order to expose the HoC.**SideBar**: For `withFassets()` to operate,`<FassetsContext.Provider>` must be rendered at the root of yourapplication DOM.  This is really a moot point, because**feature-u** automatically performs this initialization, so youreally don't have to worry about this detail _(automatingconfiguration is a Hallmark of **feature-u** - reducing boilerplatecode)_.**Please Note** this function uses named parameters.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>mapFassetsToProps</td><td><a href="#mapFassetsToPropsStruct"><code>mapFassetsToPropsStruct</code></a> | <a href="#mapFassetsToPropsFn"><code>mapFassetsToPropsFn</code></a></td><td><p>the structure defining the prop/fassetsKey
mapping, from which fasset resources are injected into
<code>component</code>.  This can either be a direct structure
({{book.api.mapFassetsToPropsStruct}}) or a function returning the
structure ({{book.api.mapFassetsToPropsFn}}).</p>
</td>
    </tr><tr>
    <td>[component]</td><td>ReactComp</td><td><p>optionally, the React Component to
be wrapped <em>(see discussion above)</em>.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: HoC \| HoF - either the HoC (the "wrapped" Component) when`component` is supplied, otherwise the HoF _(see discussionabove)_.**Examples**:1. Inject fasset resources from a **static structure**   ({{book.api.mapFassetsToPropsStruct}}), **auto wrapping** the   MainPage Component ...    ```js   function MainPage({Logo, mainLinks, mainBodies}) {     return (       <div>         <div>           <Logo/>         </div>         <div>           {mainLinks.map( ([fassetsKey, MainLink]) => <MainLink key={fassetsKey}/>)}         </div>         <div>           {mainBodies.map( (MainBody, indx) => <MainBody key={indx}/>)}         </div>       </div>     );   }      export default withFassets({     component: MainPage,  // NOTE: auto wrap MainPage     mapFassetsToProps: {   // NOTE: static structure (mapFassetsToPropsStruct)       Logo:       'company.logo',                   // Logo:  companyLogoResource,       mainLinks:  'MainPage.*.link@withKeys',                   // mainLinks:  [['MainPage.cart.link',   cartLinkResource],                   //              ['MainPage.search.link', searchLinkResource]],       mainBodies: 'MainPage.*.body'                   // mainBodies: [cartBodyResource, searchBodyResource],     }   });   ```   2. Inject fasset resources from a **functional directive**   ({{book.api.mapFassetsToPropsFn}}), **returning the HoF** -   immediately invoked ...      ```js   function MainPage({mainLinks, mainBodies}) {     return (       ... same as prior example     );   }      export default withFassets({     mapFassetsToProps(ownProps) { // NOTE: functional directive (mapFassetsToPropsFn)       ... some conditional logic based on ownProps       return {         Logo:       'company.logo',                     // Logo:  companyLogoResource,                  mainLinks:  'MainPage.*.link@withKeys',                     // mainLinks:  [['MainPage.cart.link',   cartLinkResource],                     //              ['MainPage.search.link', searchLinkResource]],         mainBodies: 'MainPage.*.body'                     // mainBodies: [cartBodyResource, searchBodyResource],       };     }   })(MainPage); // NOTE: immediately invoke the HoF, emitting the wrapped MainPage Component   ```  

<br/><br/><br/>

<a id="createAspect"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  createAspect(name, [genesis], [validateFeatureContent], [expandFeatureContent], [assembleFeatureContent], [assembleAspectResources], [initialRootAppElm], [injectRootAppElm], [injectParamsInHooks], [config], [additionalMethods]) ⇒ [`Aspect`](#Aspect)</h5>
Create an {{book.api.Aspect}} object, used to extend **feature-u**.The {{book.api.Aspect}} object promotes a series of life-cyclemethods that **feature-u** invokes in a controlled way.  Thislife-cycle is controlled by {{book.api.launchApp}} _... it issupplied the Aspects, and it invokes their methods._The essential characteristics of a typical {{book.api.Aspect}}life-cycle is to:- accumulate {{book.api.AspectContent}} across all features- perform the desired setup and configuration- expose the framework in some way _(by injecting a component in the  root DOM, or some {{book.guide.extending_aspectCrossCommunication}}  mechanism)_The {{book.guide.extending}} section provides more insight on how{{book.api.Aspect}}s are created and used.Aspect Plugins have NO one specific method that is required.  Ratherthe requirement is to **specify something** _(so as to not have anempty plugin that does nothing)_.Please refer to the **"No Single Aspect Methodis Required"** discussion in the{{book.guide.extending_aspectLifeCycleMethods}}.**Please Note** this function uses named parameters.  The order inwhich these items are presented represents the same order they areexecuted.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>name</td><td>string</td><td><p>the <code>Aspect.name</code> is used to &quot;key&quot;
{{book.api.AspectContent}} of this type in the {{book.api.Feature}}
object. <br/></p>
<p>For example: an <code>Aspect.name: &#39;xyz&#39;</code> would permit a <code>Feature.xyz:
xyzContent</code> construct.<br/></p>
<p>As a result, Aspect names cannot clash with built-in aspects, and
they must be unique <em>(across all aspects that are in-use)</em>.<br/></p>
<p>The <code>Aspect.name</code> is required, primarily for identity
purposes <em>(in logs and such)</em>.</p>
</td>
    </tr><tr>
    <td>[genesis]</td><td><a href="#genesisMeth"><code>genesisMeth</code></a></td><td><p>a Life Cycle Hook invoked
one time, at the very beginning of the app&#39;s start up process.
This hook can perform Aspect related <strong>initialization</strong> and
<strong>validation</strong>:</p>
</td>
    </tr><tr>
    <td>[validateFeatureContent]</td><td><a href="#validateFeatureContentMeth"><code>validateFeatureContentMeth</code></a></td><td><p>a
validation hook allowing this aspect to verify it&#39;s content on the
supplied feature (which is known to contain this aspect).</p>
</td>
    </tr><tr>
    <td>[expandFeatureContent]</td><td><a href="#expandFeatureContentMeth"><code>expandFeatureContentMeth</code></a></td><td><p>an
aspect expansion hook, defaulting to the algorithm defined
by {{book.api.expandWithFassets}}.<br/></p>
<p>This function rarely needs to be overridden.  It provides a hook to
aspects that need to transfer additional content from the expansion
function to the expanded content.</p>
</td>
    </tr><tr>
    <td>[assembleFeatureContent]</td><td><a href="#assembleFeatureContentMeth"><code>assembleFeatureContentMeth</code></a></td><td><p>the
Aspect method that assembles content for this aspect across all
features, retaining needed state for subsequent ops.<br/></p>
<p>This method is typically the primary task that is accomplished by
most aspects.</p>
</td>
    </tr><tr>
    <td>[assembleAspectResources]</td><td><a href="#assembleAspectResourcesMeth"><code>assembleAspectResourcesMeth</code></a></td><td><p>an
Aspect method that assemble resources for this aspect
across all other aspects, retaining needed state for subsequent
ops.<br/></p>
<p>This hook is executed after all the aspects have assembled their
feature content (i.e. after
{{book.api.assembleFeatureContentMeth}}).</p>
</td>
    </tr><tr>
    <td>[initialRootAppElm]</td><td><a href="#initialRootAppElmMeth"><code>initialRootAppElmMeth</code></a></td><td><p>a
callback hook that promotes some characteristic of this aspect
within the <code>rootAppElm</code> ... the top-level react DOM that represents
the display of the entire application.<br/></p>
<p>The {{book.guide.extending_definingAppElm}} section highlights when
to use {{book.api.initialRootAppElmMeth}} verses
{{book.api.injectRootAppElmMeth}}.</p>
</td>
    </tr><tr>
    <td>[injectRootAppElm]</td><td><a href="#injectRootAppElmMeth"><code>injectRootAppElmMeth</code></a></td><td><p>a
callback hook that promotes some characteristic of this aspect
within the <code>rootAppElm</code> ... the top-level react DOM that represents
the display of the entire application.<br/></p>
<p>The {{book.guide.extending_definingAppElm}} section highlights when
to use {{book.api.initialRootAppElmMeth}} verses
{{book.api.injectRootAppElmMeth}}.</p>
</td>
    </tr><tr>
    <td>[injectParamsInHooks]</td><td><a href="#injectParamsInHooksMeth"><code>injectParamsInHooksMeth</code></a></td><td><p>an
Aspect method that promotes <code>namedParams</code> into the
feature&#39;s {{book.guide.appLifeCycles}}, from this aspect.<br/>
This hook is executed after all aspects have assembled their
feature content (i.e. after
{{book.api.assembleFeatureContentMeth}}).</p>
</td>
    </tr><tr>
    <td>[config]</td><td>Any</td><td><p>a sub-object that can be used for
any type of configuration that a specific Aspect may need <em>(see:
{{book.guide.aspectConfig}})</em>.</p>
</td>
    </tr><tr>
    <td>[additionalMethods]</td><td>Any</td><td><p>additional methods (proprietary to
specific Aspects), supporting
{{book.guide.extending_aspectCrossCommunication}} ... a contract
between one or more aspects <em>(see:
{{book.guide.additionalMethods}})</em>.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: [`Aspect`](#Aspect) - a new Aspect object (to be consumed by {{book.api.launchApp}}).  

<br/><br/><br/>

<a id="extendAspectProperty"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  extendAspectProperty(name, owner)</h5>
Extend valid Aspect properties to include the supplied name... used when extending APIs for{{book.guide.extending_aspectCrossCommunication}}.**feature-u** keeps track of the agent that owns this extension(using the owner parameter).  This is used to prevent exceptionswhen duplicate extension requests are made by the same owner.  Thiscan happen when multiple instances of an aspect type are supported,and also in unit testing.

**Throws**:

- Error when supplied name is already reserved by a different owner

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>name</td><td>string</td><td><p>the property name to extend.</p>
</td>
    </tr><tr>
    <td>owner</td><td>string</td><td><p>the requesting owner id of this extension
request.  Use any string that uniquely identifies your utility
<em>(such as the aspect&#39;s npm package name)</em>.</p>
</td>
    </tr>  </tbody>
</table>


<br/><br/><br/>

<a id="Fassets"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  Fassets : Object</h5>
The `fassets` object _(emitted from {{book.api.launchApp}})_ isan accumulation of **public feature assets gathered from allfeatures**.  It facilitates {{book.guide.crossCom}} by promotingthe public resources of any given feature.**SideBar**: The term `fassets` is a play on words.  While it ispronounced "facet" _and is loosely related to this term_, it isspelled fassets (i.e. feature assets).There are 3 different ways to reference the resources containedin the `fassets` object:1. You may directly dereference them. As an example, an   '`action.openView`' resource can be dereferenced as follows:   ```js   fassets.action.openView('mainView');   ```2. You may use the {{book.api.Fassets_get}} method, which   can collect multiple resources (using {{book.guide.crossCom_wildcards}}).3. Your UI components may indirectly access `fassets` resources   through the {{book.api.withFassets}} Higher-order Component   (HoC).**SideBar**: There are several ways to get a handle to the`fassets` object _(see{{book.guide.crossCom_obtainingFassetsObject}})_.For more information, please refer to {{book.guide.crossCom}} and{{book.guide.crossCom_fassetsBasics}}.


* [Fassets](#Fassets) : Object
    * [.get(fassetsKey)](#Fassets.get) ⇒ resource \| Array.&lt;resource&gt;
    * [.hasFeature(featureName)](#Fassets.hasFeature) ⇒ boolean


<br/><br/><br/>

<a id="Fassets_get"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  Fassets.get(fassetsKey) ⇒ resource \| Array.&lt;resource&gt;</h5>
Get (i.e. fetch) the resource(s) corresponding to the supplied`fassetsKey`.The `fassets.get()` method is an alternative to directlydereferencing the `fassets` object ... the advantage being: 1. it can accumulate a series of resources (when    {{book.guide.crossCom_wildcards}} are used) 2. and it can more gracefully return undefined at any level    within the federated namespace pathRegarding the `fassetsKey`:- It is case-sensitive _(as are the defined resources)_.- It may contain {{book.guide.crossCom_wildcards}} (`*`), resulting in a  multiple resources being returned (a resource array), matching the  supplied pattern- Matches are restricted to the actual fassetKeys registered through  the {{book.api.fassetsAspect}} `define`/`defineUse` directives.  In  other words, the matching algorithm will **not** drill into the  resource itself (assuming it is an object with depth).- The special **dot** keyword (`'.'`) will return the fassets  object itself _(in the same tradition as "current directory")_.- `'@withKeys'`:  In some cases, you may wish to know the corresponding  `fassetsKey` of the returned resource.  This is especially true  when multiple resources are returned _(using wildcards)_.  As  an example, JSX requires unique keys for array injections _(the  `fassetsKey` is a prime candidate for this, since it is  guaranteed to be unique)_.  To accomplish this, simply suffix the `fassetsKey` with the  keyword: `'@withKeys'`.  When this is encountered, the  resource returned is a two-element array: `[fassetsKey,  resource]`.  _**SideBar**: We use this suffix technique (as  opposed to an additional parameter) to be consistent with how  {{book.api.withFassets}} operates._**SideBar**: The `fassets.get()` method is the basis of both the{{book.api.useFassets}} {{book.ext.reactHook}}, and the{{book.api.withFassets}} Higher-order Component (HoC).

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>fassetsKey</td><td>string</td><td><p>the key of the resource(s) to fetch.
This may include wildcards (<code>*</code>), as well as the <code>&#39;@withKeys&#39;</code>
suffix <em>(see discussion above)</em>.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: resource \| Array.&lt;resource&gt; - the requested fassets resource(s).- **without wildcards**, a single resource is returned  _(`undefined` for none)_.  ```js  'a.b.c':          abcResource  'a.b.c@withKeys': ['a.b.c', abcResource]  ```- **with wildcards**, the return is a resource array, in order  of feature expansion _(empty array for none)_.  ```js  'a.*':          [ab1Resource, ab2Resource, ...]  'a.*@withKeys': [ ['a.b1', ab1Resource], ['a.b2', ab2Resource], ... ]  ```  

<br/><br/><br/>

<a id="Fassets_hasFeature"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  Fassets.hasFeature(featureName) ⇒ boolean</h5>
Return an indicator as to whether the supplied feature isactive or not.**Note**: As an alternative to using this method, you canconditionally reason over the existence of "well-known fassetresources" specific to a given feature.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>featureName</td><td>string</td><td><p>the name of the feature to check.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: boolean - **true**: is active, **false**: is not active(or doesn't exist).  

<br/><br/><br/>

<a id="Feature"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  Feature : Object</h5>
The Feature object is merely a lightweight container that holds{{book.api.AspectContent}} of interest to **feature-u**.Each feature within an application promotes a Feature object (using{{book.api.createFeature}}) which catalogs the aspects of that feature.Ultimately, all Feature objects are consumed by{{book.api.launchApp}}.Feature content are simple key/value pairs (the key being anAspect.name with values of AspectContent).  These aspects caneither be **built-in** (from core **feature-u**), or **extensions**.Here is an example:```jsexport default createFeature({  name:     'featureA', // builtin aspect (name must be unique across all features within app)  enabled:  true,       // builtin aspect enabling/disabling feature  fassets: {            // builtin aspect promoting Public Face - Cross Feature Communication    define: {      'api.openA':  () => ...,      'api.closeA': () => ...,    },  },  appWillStart: (...) => ..., // builtin aspect (Application Life Cycle Hook)  appInit:      (...) => ..., // ditto  appDidStart:  (...) => ..., // ditto  reducer: ..., // feature redux reducer (extended aspect from the feature-redux plugin)  logic:   ..., // feature logic modules (extended aspect from the feature-redux-logic plugin)});```For more information, please refer to{{book.guide.detail_featureAndAspect}}.


<br/><br/><br/>

<a id="appWillStartCB"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  appWillStartCB ⇒ reactElm \| void</h5>
An optional {{book.guide.appLifeCycle}} invoked one time, veryearly in the app startup process.This life-cycle hook can do any type of general app-specificinitialization _(for example initializing a **PWA serviceworker**)_.In addition, it can optionally inject static content in the app'sDOM root.  Any return is interpreted as the app's new `rootAppElm`_(an accumulative process)_.  **IMPORTANT**: When this is used, thesupplied `curRootAppElm` MUST be included as part of thisdefinition (accommodating the accumulative process of other featureinjections)! **More information is available at{{book.guide.injectingDomContent}}**For more information _(with examples)_, please refer to theGuide's {{book.guide.appWillStart}}.**Please Note** this function uses named parameters.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>fassets</td><td><a href="#Fassets"><code>Fassets</code></a></td><td><p>the Fassets object used in cross-feature-communication.</p>
</td>
    </tr><tr>
    <td>curRootAppElm</td><td>reactElm</td><td><p>the current react app element
root.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: reactElm \| void - optionally, new top-level content (which in turnmust contain the supplied `curRootAppElm`).  Use a void returnwhen top-level content is unchanged.  

<br/><br/><br/>

<a id="appInitCB"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  appInitCB ⇒ Promise \| void</h5>
An optional {{book.guide.appLifeCycle}} invoked one time, later inthe app startup process.  It supports blocking asyncinitialization.This hook is invoked when the app is **nearly up-and-running**.- The {{book.guide.detail_reactRegistration}} has already occurred  _(via the {{book.api.registerRootAppElmCB}} callback)_.  As a  result, you can rely on utilities that require an app-specific  `rootAppElm` to exist.- You have access to the `getState()` and `dispatch()` function,  assuming you are using {{book.ext.redux}} (when detected by  **feature-u**'s plugable aspects).  These parameters are actually injected by the  {{book.ext.featureRedux}} Aspect, and are examples of what can be  injected by any Aspect _(please refer your specific Aspect's  documentation to determine other parameters)_.Just like the {{book.api.appWillStartCB}} hook, you may perform anytype of general initialization that is required by your feature.However the **hallmark of this hook** is **you can block for anyasynchronous initialization to complete**.  By simply returning apromise, **feature-u** will wait for the process to complete.The user is kept advised of any long-running async processes.  Bydefault an `'initializing feature: {feature.name}'` message isused, but you can customize it through the supplied{{book.api.showStatusCB}} function parameter.For more info with examples, please see the Guide's{{book.guide.appInit}}.**Please Note** this function uses named parameters.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>showStatus</td><td><a href="#showStatusCB"><code>showStatusCB</code></a></td><td><p>the function that (when invoked)
will communicate a blocking &quot;persistent&quot; status message to the end
user.</p>
</td>
    </tr><tr>
    <td>fassets</td><td><a href="#Fassets"><code>Fassets</code></a></td><td><p>the Fassets object used in cross-feature-communication.</p>
</td>
    </tr><tr>
    <td>[getState]</td><td>Any</td><td><p>the redux function returning the top-level
app state (when redux is in use).</p>
</td>
    </tr><tr>
    <td>[dispatch]</td><td>function</td><td><p>the redux dispatch() function (when
redux is in use).</p>
</td>
    </tr><tr>
    <td>[injectedAspectParams]</td><td>any</td><td><p>additional parameters
injected by Aspect plugins <em>(please refer your specific Aspect&#39;s
documentation to determine other parameters)</em>.  The <code>getState</code> and
<code>dispatch</code> params (above) are examples of this.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: Promise \| void - optionally, a promise (for asynchronousprocesses) - and feature-u will wait for the process to complete.Use a void return (for synchronous processes) - and no blockingwill occur.  

<br/><br/><br/>

<a id="appDidStartCB"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  appDidStartCB ⇒</h5>
An optional {{book.guide.appLifeCycle}} invoked one time,once the app startup process has completed.This life-cycle hook can be used to trigger **"the app isrunning"** events.  A typical usage is to **"kick start"** someearly application logic.Because the app is up-and-running at this time, you have access tothe `getState()` and `dispatch()` function ... assuming you are using{{book.ext.redux}} (when detected by **feature-u**'s plugable aspects).These parameters are actually injected by the{{book.ext.featureRedux}} Aspect, and are examples of what can beinjected by any Aspect _(please refer your specific Aspect'sdocumentation to determine other parameters)_.For more info with examples, please see the Guide's{{book.guide.appDidStart}}.**Please Note** this function uses named parameters.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>fassets</td><td><a href="#Fassets"><code>Fassets</code></a></td><td><p>the Fassets object used in cross-feature-communication.</p>
</td>
    </tr><tr>
    <td>[getState]</td><td>Any</td><td><p>the redux function returning the top-level
app state (when redux is in use).</p>
</td>
    </tr><tr>
    <td>[dispatch]</td><td>function</td><td><p>the redux dispatch() function (when
redux is in use).</p>
</td>
    </tr><tr>
    <td>[injectedAspectParams]</td><td>any</td><td><p>additional parameters
injected by Aspect plugins <em>(please refer your specific Aspect&#39;s
documentation to determine other parameters)</em>.  The <code>getState</code> and
<code>dispatch</code> params (above) are examples of this.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: void  

<br/><br/><br/>

<a id="fassets"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  fassets : BuiltInAspect</h5>
A builtin aspect that publicly promotes feature-based resourcescalled `fassets` (feature assets).  These resources are the basisof {{book.guide.crossCom}}. You can think of this as the Public Faceof a feature.**SideBar**: The term `fassets` is a play on words.  While it ispronounced "facet" _and is loosely related to this term_, it isspelled fassets (i.e. feature assets).Feature resources are accumulated across all features, and exposedthrough the {{book.api.FassetsObject}}.  They can also be referencedvia the {{book.api.withFassets}} HoC.The `fassets` aspect can both define resources, and/or declare aresource contract (i.e. the intention to use a set of fassetresources).  This is accomplished via three separate `fassets`directives: `define`, `use`, and `defineUse`.  A good summary ofthese directives can be found at{{book.guide.crossCom_fassetsRecapPushOrPull}}.1. **define**: define public resources, held in the   {{book.api.FassetsObject}}      ```js   fassets: {     define: {       '{fassetsKey}': {fassetsValue}          ...           NOTES:        - fassetsKey MUST be unique        - are case-sensitive        - may contain federated namespace (via dots ".")          ... normalized in fassets object          ... ex: 'MainPage.launch'        - may be any valid JS identifier (less $ support)        - may NOT contain wildcards          ... i.e. must be defined completely       // examples ...       'openView': actions.view.open, // fassets.openView(viewName): Action          // federated namespace example       'selector.currentView': selector.currentView, // fassets.selector.currentView(appState): viewName          // UI Component example       'MainPage.cart.link': () => <Link to="/cart">Cart</Link>,       'MainPage.cart.body': () => <Route path="/cart" component={ShoppingCart}/>,     }   }   ```   2. **use**: specify public resource keys that will be **used** by the   containing feature (i.e. a resource contract)      ```js   fassets: {     use: [       '{fassetsKey}',       -or-       ['$fassetsKey', {required: true/false, type: $validationFn}],          ...           NOTES:        - each key will be supplied by other features        - this is a communication to other features (i.e. a contract)          ... saying: I plan to "use" these injections          HOWEVER: feature-u cannot strictly enforce this usage                   ... enclosed feature should reference this                       {fassetsKey} through fassets.get(), or withFassets()        - is case-sensitive        - may contain federated namespace (with dots ".")          ... ex: 'MainPage.launch'        - may be any valid JS identifier (less $ support)        - may contain wildcards (with "*")          ... ex: 'MainPage.*.link'       // examples ...       'MainPage.launch',             // may contain wildcards ...       'MainPage.*.link',       'MainPage.*.body',             // optionally supply options object, controlling optionality and data types       ['MainPage.*.link',  { required: true,   type: any  }], // same as DEFAULTS       ['MainPage.*.link',  { required: false,             }], // optional of any type       ['MainPage.*.link',  {                   type: comp }], // required of react component type       ['MainPage.*.link',  { required: false,  type: comp }], // optional of react component type     ]   }   ```   3. **defineUse**: define public resources specified by other features (via   the `use` directive)      ```js   fassets: {     defineUse: {       '{fassetsKey}': {fassetsValue}          ...           NOTES:        - this is identical to fassets.define EXCEPT:        - it MUST MATCH a fassets.use directive          ... using this directive, feature-u will perform additional              validation to unsure these entries match a use contract          // examples ...       'MainPage.cart.link': () => <Link to="/cart">Cart</Link>,       'MainPage.cart.body': () => <Route path="/cart" component={ShoppingCart}/>,     }   }   ```For more information, please refer to {{book.guide.crossCom}},{{book.api.FassetsObject}}, the {{book.api.withFassets}} HoC,and the {{book.guide.crossCom_fassetsRecapPushOrPull}}.


<br/><br/><br/>

<a id="expandWithFassetsCB"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  expandWithFassetsCB ⇒ [`AspectContent`](#AspectContent)</h5>
A "managed expansion callback" (defined by{{book.api.expandWithFassets}}) that when invoked (by **feature-u**)expands and returns the desired {{book.api.AspectContent}}.**For more information _(with examples)_**, please refer to{{book.guide.crossCom_managedCodeExpansion}}.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>fassets</td><td><a href="#Fassets"><code>Fassets</code></a></td><td><p>the Fassets object used in cross-feature-communication.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: [`AspectContent`](#AspectContent) - The desired AspectContent (ex: reducer,logic module, etc.).  

<br/><br/><br/>

<a id="fassetValidations"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  fassetValidations : Object</h5>
A pre-defined container of fasset validation functions, which canbe employed in the {{book.api.fassetsAspect}} `use` directive.This allows the `use` directive to specify data type and contentvalidation constraints.These validations are available as a convenience.  Additionalvalidations can be created as needed.The validation API should adhere to the following signature:``` + fassetValidationFn(fassetsValue): string || null```A return value of null represents a valid value, while a stringspecifies a validation error that feature-u will format as follows(see ${returnStr}):```  VALIDATION ERROR in resource: '${fassetsKey}',    expecting: ${returnStr} ...     resource defined in Feature: '${resource.definingFeature}',    usage contract '${useKey}' found in Feature: '${featureName}'```The following pre-defined validations are promoted through `fassetValidations`: - `any`:  any type (except undefined) - `comp`: a react component - `fn`:   a function - `str`:  a string - `bool`: a boolean**Example**:```jscreateFeature({  fassets: {    use: [       'MainPage.*.link', // DEFAULT: required of type any      ['MainPage.*.body', {required: false, type: fassetValidations.comp}],    ],  },});```


<br/><br/><br/>

<a id="registerRootAppElmCB"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  registerRootAppElmCB ⇒</h5>
The {{book.api.launchApp}} callback hook that registers thesupplied root application element to the specific React frameworkused in the app.Because this registration is accomplished by app-specific code,**feature-u** can operate in any of the React platforms, such as:{{book.ext.react}} web, {{book.ext.reactNative}},{{book.ext.expo}}, etc.Please refer to {{book.guide.detail_reactRegistration}} for moredetails and complete examples.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>rootAppElm</td><td>reactElm</td><td><p>the root application element to be
registered.</p>
</td>
    </tr><tr>
    <td>fassets</td><td><a href="#Fassets"><code>Fassets</code></a></td><td><p>the Fassets object used in cross-feature-communication
(rarely needed except to allow client to inject their own
FassetsContext.Provider for a null rootAppElm).</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: void  

<br/><br/><br/>

<a id="showStatusCB"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  showStatusCB ⇒</h5>
The optional {{book.api.launchApp}} callback hook that communicatesa blocking "persistent" status message to the end user.These status messages originate from the blocking that occurs inthe asynchronous processes managed by the {{book.guide.appInitCB}}life-cycle-hook.By design **feature-u** has no ability to manifest messages to theend user, because this is very app-specific in styling and otherheuristics.  By default (when **NO** `showStatus` parameter issupplied, **feature-u** will simply **console log** these messages.A typical manifestation of this callback is to display a runningpersistent SplashScreen, seeded with the supplied message. TheSplashScreen should be taken down when NO message is supplied(i.e. `''`).Please refer to {{book.guide.appInitCB}} for more details andexamples.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>[msg]</td><td>string</td><td><p>the &quot;persistent&quot; message to display.  When
NO message is supplied (i.e. <code>&#39;&#39;</code>), <strong>all</strong> user notifications
should be cleared <em>(for example, take the SplashScreen down)</em>.</p>
</td>
    </tr><tr>
    <td>[err]</td><td>Error</td><td><p>an optional error to communicate to the
user.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: void  

<br/><br/><br/>

<a id="mapFassetsToPropsStruct"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  mapFassetsToPropsStruct : Object</h5>
A structure (used by {{book.api.withFassets}} and  {{book.api.useFassets}}) defining aprop/fassetsKey mapping, from which fasset resources are injectedinto a Component.  Please see {{book.guide.crossCom_uiComposition}}for examples.The injected Component properties will reference the fassetresource corresponding to the `fassetsKey`.Each `fassetsKey` is case-sensitive _(as are the defined resources)_.Matches are restricted to the actual fassetKeys registered throughthe {{book.api.fassetsAspect}} `define`/`defineUse` directives.  Inother words, the matching algorithm will **not** drill into theresource itself (assuming it is an object with depth).The special **dot** keyword (`'.'`) will yield the fassets objectitself _(in the same tradition as "current directory")_.  This isuseful if you wish to inject fassets into downstream processes(such as redux `connect()` via it's `ownProps`).**Wildcards**{{book.guide.crossCom_wildcards}} (`*`) are supported in thefassetsKey, accumulating multiple resources (a resource array),matching the supplied pattern:- **without wildcards**, a single resource is injected  _(`undefined` for none)_.- **with wildcards**, a resource array is injected, in order of  feature expansion _(empty array for none)_._Example ..._```jsmapFassetsToProps: {  Logo:       'company.logo',              // Logo:  companyLogoResource,              // NOTE: wildcard usage ...  mainLinks:  'MainPage.*.link',              // mainLinks:  [cartLinkResource, searchLinkResource],  mainBodies: 'MainPage.*.body'              // mainBodies: [cartBodyResource, searchBodyResource],}```**@withKeys**In some cases, you may wish to know the corresponding`fassetsKey` of the returned resource.  This is especially truewhen multiple resources are returned _(using wildcards)_.As an example, React requires a `key` attribute for arrayinjections _(the `fassetsKey` is a prime candidate for this, sinceit is guaranteed to be unique)_.To accomplish this, simply suffix the `fassetsKey` with thekeyword: `'@withKeys'`.  When this is encountered, the resourcereturned is a two-element array: `[fassetsKey, resource]`._Example ..._```jsmapFassetsToProps: {  Logo:       'company.logo',              // Logo:  companyLogoResource,  mainLinks:  'MainPage.*.link@withKeys', // NOTE: @withKeys directive              // mainLinks:  [['MainPage.cart.link',   cartLinkResource],              //              ['MainPage.search.link', searchLinkResource]],  mainBodies: 'MainPage.*.body'              // mainBodies: [cartBodyResource, searchBodyResource],}```This topic is discussed in more detail in: {{book.guide.crossCom_reactKeys$}}.


<br/><br/><br/>

<a id="mapFassetsToPropsFn"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  mapFassetsToPropsFn ⇒ [`mapFassetsToPropsStruct`](#mapFassetsToPropsStruct)</h5>
A function (used by {{book.api.withFassets}}) that returns a{{book.api.mapFassetsToPropsStruct}}, defining a prop/fassetsKeymapping, from which fasset resources are injected into a Component.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>ownProps</td><td>obj</td><td><p>the outlying properties supplied to the
connected component.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: [`mapFassetsToPropsStruct`](#mapFassetsToPropsStruct) - the structure defining aprop/fassetsKey mapping, from which fasset resources are injectedinto a Component.  

<br/><br/><br/>

<a id="Aspect"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  Aspect : Object</h5>
Aspect objects (emitted from {{book.api.createAspect}}) are used toextend **feature-u**.The Aspect object promotes a series of life-cycle methods that**feature-u** invokes in a controlled way.  This life-cycle iscontrolled by {{book.api.launchApp}} _... it is supplied theAspects, and it invokes their methods._Typically Aspects are packaged separately _(as an external npm**feature-u** extension)_, although they can be created locallywithin a project _(if needed)_.For more information, please refer to{{book.guide.detail_extendableAspects}} and{{book.guide.extending}}.


<br/><br/><br/>

<a id="AspectContent"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  AspectContent : Any</h5>
The content (or payload) of an {{book.api.Aspect}}, specifiedwithin a {{book.api.Feature}}.The content type is specific to the Aspect. For example, a reduxAspect assembles reducers (via `Feature.reducer`), while aredux-logic Aspect gathers logic modules (via `Feature.logic`),etc.AspectContent can either be defined from **built-in** aspects_(via core **feature-u**)_, or **extensions** _(from{{book.api.Aspect}})_.An {{book.api.Aspect}} object extends **feature-u** by accumulatinginformation of interest from {{book.api.Feature}} objects _(indexedby the Aspect name)_.**Note**: Whenever AspectContent definitions require the {{book.api.FassetsObject}} **at code expansion time**, you can wrap thedefinition in a {{book.api.expandWithFassets}} function.  In otherwords, your aspect content can either be the actual content itself_(ex: a reducer)_, or a function that returns the content.For more information, please refer to{{book.guide.detail_featureAndAspect}}.


<br/><br/><br/>

<a id="genesisMeth"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  genesisMeth ⇒ string</h5>
A Life Cycle Hook invoked one time, at the very beginning ofthe app's start up process.**Antiquated Note**:- The `genesis()` hook is somewhat antiquated, relegated to Aspects  that are promoted as singletons.  In this scenario, client-side  configuration could be introduced after instantiation _(by adding  content to {{book.guide.aspectConfig}})_, while still allowing  **initialization** and **validation** to occur early in the startup  process _(via this `genesis()` hook)_.- A better alternative to the `genesis()` hook is to promote your  {{book.guide.extending_customAspectPlugins}} as non-singletons,  where **initialization** and **validation** can be directly promoted  though the plugin constructor.The `genesis()` hook can perform Aspect related **initialization** and**validation**:- **initialization**: It is possible to to register proprietary  Aspect/Feature APIs in the `genesis()` hook ... via  {{book.api.extendAspectProperty}} and  {{book.api.extendFeatureProperty}} _(please see:  {{book.guide.extending_aspectCrossCommunication}} and  {{book.guide.crossCom}})_.  The preferred place to do this initialization is in the plugin  constructor _(see **Antiquated Note** above)_.- **validation**: It is possible to perform Aspect validation in the  `genesis()` hook ... say for required configuration properties  injected by the client after instantiation.  This is the reason for  the optional return string.  The preferred place to do validation is in the plugin constructor,  gathering this information as constructor parameters _(see  **Antiquated Note** above)_.**API:** {{book.api.genesisMeth$}}

**Returns**: string - an error message when self is in an invalid state(falsy when valid).  Because this validation occurs under thecontrol of {{book.api.launchApp}}, any message is prefixed with:`'launchApp() parameter violation: '`.  

<br/><br/><br/>

<a id="validateFeatureContentMeth"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  validateFeatureContentMeth ⇒ string</h5>
A validation hook allowing this aspect to verify it's content onthe supplied feature.**API:** {{book.api.validateFeatureContentMeth$}}

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>feature</td><td><a href="#Feature"><code>Feature</code></a></td><td><p>the feature to validate, which is known
to contain this aspect.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: string - an error message string when the supplied featurecontains invalid content for this aspect (falsy when valid).Because this validation conceptually occurs under the control of{{book.api.createFeature}}, any message is prefixed with:`'createFeature() parameter violation: '`.  

<br/><br/><br/>

<a id="expandFeatureContentMeth"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  expandFeatureContentMeth ⇒ string</h5>
Expand self's {{book.api.AspectContent}} in the supplied feature,replacing that content (within the feature).  Once expansion iscomplete, **feature-u** will perform a delayed validation of theexpanded content.**API:** {{book.api.expandFeatureContentMeth$}}The default behavior simply implements the expansion algorithmdefined by {{book.api.expandWithFassets}}:```jsfeature[this.name] = feature[this.name](fassets);```This default behavior rarely needs to change.  It however providesa hook for aspects that need to transfer additional content fromthe expansion function to the expanded content.  As an example, the`reducer` aspect must transfer the slice property from theexpansion function to the expanded reducer.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>fassets</td><td><a href="#Fassets"><code>Fassets</code></a></td><td><p>the Fassets object used in feature
cross-communication.</p>
</td>
    </tr><tr>
    <td>feature</td><td><a href="#Feature"><code>Feature</code></a></td><td><p>the feature which is known to contain
this aspect <strong>and</strong> is in need of expansion (as defined by
{{book.api.expandWithFassets}}).</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: string - an optional error message when the suppliedfeature contains invalid content for this aspect (falsy whenvalid).  This is a specialized validation of the expansionfunction, over-and-above what is checked in the standard{{book.api.validateFeatureContentMeth}} hook.  

<br/><br/><br/>

<a id="assembleFeatureContentMeth"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  assembleFeatureContentMeth ⇒</h5>
The Aspect method that assembles content for this aspectacross all features, retaining needed state for subsequent ops.This method is typically the primary task that is accomplished bymost aspects.**API:** {{book.api.assembleFeatureContentMeth$}}

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>fassets</td><td><a href="#Fassets"><code>Fassets</code></a></td><td><p>the Fassets object used in feature
cross-communication.</p>
</td>
    </tr><tr>
    <td>activeFeatures</td><td><a href="#Feature"><code>Array.&lt;Feature&gt;</code></a></td><td><p>The set of active (enabled)
features that comprise this application.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: void  

<br/><br/><br/>

<a id="assembleAspectResourcesMeth"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  assembleAspectResourcesMeth ⇒</h5>
An Aspect method that assembles resources for this aspectacross all other aspects, retaining needed state for subsequentops.  This hook is executed after all the aspects have assembledtheir feature content (i.e. after{{book.api.assembleFeatureContentMeth}}).**API:** {{book.api.assembleAspectResourcesMeth$}}This is an optional second-pass (so-to-speak) of Aspect datagathering, that facilitates{{book.guide.extending_aspectCrossCommunication}}.  It allows anextending aspect to gather resources from other aspects, using anadditional API (ex: `Aspect.getXyz()`).

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>fassets</td><td><a href="#Fassets"><code>Fassets</code></a></td><td><p>the Fassets object used in feature
cross-communication.</p>
</td>
    </tr><tr>
    <td>aspects</td><td><a href="#Aspect"><code>Array.&lt;Aspect&gt;</code></a></td><td><p>The set of <strong>feature-u</strong> Aspect objects
used in this this application.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: void  

<br/><br/><br/>

<a id="initialRootAppElmMeth"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  initialRootAppElmMeth ⇒ reactElm</h5>
A callback hook that promotes some characteristic of thisaspect within the `rootAppElm` ... the top-level react DOM thatrepresents the display of the entire application.**API:** {{book.api.initialRootAppElmMeth$}}The {{book.guide.extending_definingAppElm}} section highlights whento use {{book.api.initialRootAppElmMeth}} verses{{book.api.injectRootAppElmMeth}}.**NOTE**: When this hook is used, the supplied curRootAppElm MUST beincluded as part of this definition!

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>fassets</td><td><a href="#Fassets"><code>Fassets</code></a></td><td><p>the Fassets object used in feature
cross-communication.</p>
</td>
    </tr><tr>
    <td>curRootAppElm</td><td>reactElm</td><td><p>the current react app element root.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: reactElm - a new react app element root (which in turn mustcontain the supplied curRootAppElm), or simply the suppliedcurRootAppElm (if no change).  

<br/><br/><br/>

<a id="injectRootAppElmMeth"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  injectRootAppElmMeth ⇒ reactElm</h5>
A callback hook that promotes some characteristic of thisaspect within the `rootAppElm` ... the top-level react DOM thatrepresents the display of the entire application.**API:** {{book.api.injectRootAppElmMeth$}}The {{book.guide.extending_definingAppElm}} section highlights whento use {{book.api.initialRootAppElmMeth}} verses{{book.api.injectRootAppElmMeth}}.**NOTE**: When this hook is used, the supplied curRootAppElm MUST beincluded as part of this definition!

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>fassets</td><td><a href="#Fassets"><code>Fassets</code></a></td><td><p>the Fassets object used in feature
cross-communication.</p>
</td>
    </tr><tr>
    <td>curRootAppElm</td><td>reactElm</td><td><p>the current react app element root.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: reactElm - a new react app element root (which in turn mustcontain the supplied curRootAppElm), or simply the suppliedcurRootAppElm (if no change).  

<br/><br/><br/>

<a id="injectParamsInHooksMeth"></a>

<h5 style="margin: 10px 0px; border-width: 5px 0px; padding: 5px; border-style: solid;">
  injectParamsInHooksMeth ⇒ namedParams</h5>
An Aspect method that promotes `namedParams` into thefeature's {{book.guide.appLifeCycles}}, from this aspect.  Thishook is executed after all aspects have assembled their featurecontent (i.e. after {{book.api.assembleFeatureContentMeth}}).Here is a `namedParams` example from a redux aspect, promoting it'sstate and dispatch functions:```js{getState, dispatch}```**API:** {{book.api.injectParamsInHooksMeth$}}Any aspect may promote their own set of `namedParams`.  **feature-u**will insure there are no name clashes across aspects (which resultsin an exception).  If your parameter names have a high potentialfor clashing, a **best practice** would be to qualify them in someway to better insure uniqueness.

<table>
  <thead>
    <tr>
      <th>Param</th><th>Type</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
<tr>
    <td>fassets</td><td><a href="#Fassets"><code>Fassets</code></a></td><td><p>the Fassets object used in feature
cross-communication.</p>
</td>
    </tr>  </tbody>
</table>

**Returns**: namedParams - a plain object that will be injected (asnamed parameters) into the feature's {{book.guide.appLifeCycles}},from this aspect.  
