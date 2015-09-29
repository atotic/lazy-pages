# power-page
Lazily instatiated Polymer pages: iron-page + neon-animated-pages + dom-if

Functionality:

Next:
- test lazy loading. Get those <link rel="import" in the demo>
- animation transitions

Stage 1: if loading
- pages that are dom-if templates instatiated by setting if
- can mix dom-if and plain elements
- support restamp on dom-if

Stage 2: animation
- configure animation with an array
- animate transitions

DONE:
- pages that are dom-if templates instatiated by setting if
- can mix dom-if and plain elements
- support restamp on dom-if

ARCHITECTURE:
NeonAnimationRunnerBehavior
  has animationConfig to specify animations
  animationConfig also specifies node to animate, but we want node to be dynamic
  solution:

IronSelectableBehavior:
- selects element out of items. We can't do that, since our items are in flux

swithPages algorithm

switchPages:



  var exitPage, entryPage;
  var entryPage = page;

  this._currentPage = entryPage;

// does template need iron-selected? No.

// cancel existing animations

// prepare exitInstance
  exitInstance.addClass('neon-animating'); // to prevent it from display:none
  exitInstance.removeClass('iron-selected');

// prepare entryInstance
// animation starts when entryPage instance is visible
// if exitPage instance is not visible, do we care?

  async createEntryInstance -- listen to template.dom-change

  entryInstance.addClass('iron-selected')

  async animateExitInstance
    if (exitInstance && exitAnimation)
      addAnimationTo animationConfig
    if (entryInstance && entryAnimation)
      addAnimationTo animationConfig

  async playAnimation( fromPage: toPage )

  transitionComplete();
  notifyPageResize
