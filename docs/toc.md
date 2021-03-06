# Table of content 

### feature-u (3.0.0)
* [Getting Started](start.md)
  * [Install](start.md#install)
  * [Access](start.md#access)
  * [Potential Need for Polyfills](start.md#potential-need-for-polyfills)

----
* [Basic Concepts](concepts.md)
  * [Feature Based Development](concepts.md#feature-based-development)
    * [Segregating Features](concepts.md#segregating-features)
    * [Feature Goals](concepts.md#feature-goals)
      * [Feature Runtime Consolidation](concepts.md#feature-runtime-consolidation)
      * [Feature Collaboration](concepts.md#feature-collaboration)
  * [The feature-u Solution](concepts.md#the-feature-u-solution)
    * [launchApp()](concepts.md#launchapp)
    * [Feature Object](concepts.md#feature-object)
    * [aspects](concepts.md#aspects)
    * [Running the App](concepts.md#running-the-app)
      * [App Initialization](concepts.md#app-initialization)
      * [Framework Configuration](concepts.md#framework-configuration)
      * [Launching Your Application](concepts.md#launching-your-application)
    * [Cross Feature Communication](concepts.md#cross-feature-communication)
    * [Feature Based UI Composition](concepts.md#feature-based-ui-composition)
      * [Resource Contracts](concepts.md#resource-contracts)
    * [Feature Enablement](concepts.md#feature-enablement)
  * [In Summary](concepts.md#in-summary)
* [Playful Features](presentation.md)
  * [Presentation](presentation.md#presentation)
  * [Video Content](presentation.md#video-content)
  * [Presentation Resources](presentation.md#presentation-resources)
  * [Presentation Syllabus](presentation.md#presentation-syllabus)
* [Benefits](benefits.md)

----
* [Usage](usage.md)
  * [Directory Structure](usage.md#directory-structure)
  * [Feature Object](usage.md#feature-object)
  * [Feature Accumulation](usage.md#feature-accumulation)
  * [Aspect Accumulation](usage.md#aspect-accumulation)
  * [launchApp()](usage.md#launchapp)
  * [Real Example](usage.md#real-example)
* [A Closer Look](detail.md)
  * [aspects](detail.md#aspects)
  * [Feature & aspect content](detail.md#feature-object-relaying-aspect-content)
    * [Built-In aspects](detail.md#built-in-aspects)
    * [Extendable aspects](detail.md#extendable-aspects)
  * [Launching Your Application](detail.md#launching-your-application)
    * [Export fassets](detail.md#export-fassets)
    * [React Registration](detail.md#react-registration)
    * [Covert Asynchronicity](detail.md#covert-asynchronicity)
* [Application Life Cycle Hooks](appLifeCycle.md)
  * [appWillStart](appLifeCycle.md#appwillstart)
    * [Injecting DOM Content](appLifeCycle.md#injecting-dom-content)
  * [appInit](appLifeCycle.md#appinit)
  * [appDidStart](appLifeCycle.md#appdidstart)
* [Cross Feature Communication](crossCommunication.md)
  * [Basic Concepts: fassets](crossCommunication.md#basic-concepts-fassets)
    * [fassets definition](crossCommunication.md#fassets-definition)
    * [fassets usage](crossCommunication.md#fassets-usage)
    * [federated namespace](crossCommunication.md#federated-namespace)
  * [UI Composition](crossCommunication.md#ui-composition)
    * [useFassets() Hook](crossCommunication.md#usefassets-hook)
    * [withFassets() HoC](crossCommunication.md#withfassets-hoc)
    * [Resource Contracts](crossCommunication.md#resource-contracts)
    * [Wildcards](crossCommunication.md#wildcards-adding-dynamics)
      * [Wildcard Processing](crossCommunication.md#wildcard-processing)
      * [Resource Order](crossCommunication.md#resource-order-in-wildcard-processing)
      * [React Keys](crossCommunication.md#react-keys-in-array-processing)
  * [Resource Validation](crossCommunication.md#resource-validation)
  * [Does Feature Exist](crossCommunication.md#does-feature-exist)
  * [fassets recap: Push or Pull](crossCommunication.md#fassets-recap-push-or-pull)
  * [Obtaining fassets object](crossCommunication.md#obtaining-fassets-object)
    * [fassets parameter](crossCommunication.md#fassets-parameter)
    * [Obtain fassets from Hooks](crossCommunication.md#obtain-fassets-from-hooks)
    * [Inject fassets comp props](crossCommunication.md#inject-fassets-comp-props)
    * [Managed Code Expansion](crossCommunication.md#managed-code-expansion)
    * [import fassets](crossCommunication.md#import-fassets)
* [Feature Based Routes](featureRouter.md)
  * [react-router](featureRouter.md#react-router)
  * [feature-router](featureRouter.md#feature-router)
* [Feature Enablement](enablement.md)
  * [How it works](enablement.md#how-does-it-work)
  * [Existence and Dependencies](enablement.md#feature-existence-and-dependencies)
* [Best Practices](bestPractices.md)
  * [Avoid Cross Feature Imports](bestPractices.md#avoid-cross-feature-imports)
  * [Feature Name](bestPractices.md#feature-name)
  * [Feature State Location](bestPractices.md#feature-state-location)

----
* [Core API](coreApi.md)
  * [createFeature()](api.md#createFeature)
    * Built-In aspects ...
      * [fassets aspect](api.md#fassets)
      * [appWillStart()](api.md#appWillStartCB)
      * [appInit()](api.md#appInitCB)
      * [appDidStart()](api.md#appDidStartCB)
  * [expandWithFassets()](api.md#expandWithFassets)
    * [expandWithFassetsCB()](api.md#expandWithFassetsCB)
  * [launchApp()](api.md#launchApp)
    * [registerRootAppElm()](api.md#registerRootAppElmCB)
    * [showStatus()](api.md#showStatusCB)
  * [useFassets()](api.md#useFassets)
  * [withFassets()](api.md#withFassets)
    * [mapFassetsToPropsStruct](api.md#mapFassetsToPropsStruct)
    * [mapFassetsToProps()](api.md#mapFassetsToPropsFn)
  * Misc ...
    * [assertNoRootAppElm()](api.md#assertNoRootAppElm)
  * Object Refs ...
    * [Fassets](api.md#Fassets)
      * [get()](api.md#Fassets_get)
      * [hasFeature()](api.md#Fassets_hasFeature)
    * [fassetValidations](api.md#fassetValidations)
    * [Feature](api.md#Feature)
    * [Aspect](api.md#Aspect)
    * [AspectContent](api.md#AspectContent)

----
* [Extending feature-u](extending.md)
  * [Locating Extensions](extending.md#locating-extensions)
  * [Aspect Object](extending.md#aspect-object-extending-feature-u)
  * [Defining rootAppElm](extending.md#defining-rootappelm)
  * [Aspect Cross Communication](extending.md#aspect-cross-communication)
  * [Aspect Life Cycle Methods](extending.md#aspect-life-cycle-methods)
    * [name](extending.md#aspectname)
    * [genesis()](extending.md#aspectgenesis)
    * [validateFeatureContent()](extending.md#aspectvalidatefeaturecontent)
    * [expandFeatureContent()](extending.md#aspectexpandfeaturecontent)
    * [assembleFeatureContent()](extending.md#aspectassemblefeaturecontent)
    * [assembleAspectResources()](extending.md#aspectassembleaspectresources)
    * [initialRootAppElm()](extending.md#aspectinitialrootappelm)
    * [injectRootAppElm()](extending.md#aspectinjectrootappelm)
    * [injectParamsInHooks()](extending.md#aspectinjectparamsinhooks)
    * [config](extending.md#aspectconfig)
    * [additionalMethods()](extending.md#aspectadditionalmethods)
  * [Custom Aspect Plugins](extending.md#custom-aspect-plugins)
  * [Extension API](extensionApi.md)
    * [createAspect()](api.md#createAspect)
    * [extendAspectProperty()](api.md#extendAspectProperty)
    * [extendFeatureProperty()](api.md#extendFeatureProperty)
    * Object Refs ...
      * [Fassets](api.md#Fassets)
        * [get()](api.md#Fassets_get)
        * [hasFeature()](api.md#Fassets_hasFeature)
      * [fassetValidations](api.md#fassetValidations)
      * [Feature](api.md#Feature)
      * [Aspect](api.md#Aspect)
      * [AspectContent](api.md#AspectContent)

----
* [Distribution](dist.md)
* [Why feature-u?](why.md)
* [Revision History](history.md)
  * [v3.0.0 (February, 5, 2020)](history.md#v3_0_0)
    * [Full Docs](https://feature-u.js.org/3.0.0/)
  * [v2.1.1 (December 9, 2019)](history.md#v2_1_1)
    * [Full Docs](https://feature-u.js.org/2.1.1/)
  * [v2.1.0 (July 19, 2019)](history.md#v2_1_0)
    * [Full Docs](https://feature-u.js.org/2.1.0/)
  * [v2.0.0 (May 10, 2019)](history.md#v2_0_0)
    * [Full Docs](https://feature-u.js.org/2.0.0/)
  * [v1.0.1 (September 5, 2018)](history.md#v1_0_1)
    * [Full Docs](https://feature-u.js.org/1.0.1/)
  * [v1.0.0 (August 14, 2018)](history.md#v1_0_0)
    * [Full Docs](https://feature-u.js.org/1.0.0/)
    * [Migration Notes](migration.1.0.0.md)
  * [v0.1.3 (July 2, 2018)](history.md#v0_1_3)
    * [Full Docs](https://feature-u.js.org/0.1.3/)
  * [v0.1.0 (March 6, 2018)](history.md#v0_1_0)
    * [Full Docs](https://feature-u.js.org/0.1.0/)
* [MIT License](LICENSE.md)
