<script>
export default {
  name: `TransitionExpand`,
  functional: true,
  props: {
    afterEnter: {
      type: Function
    },
    afterLeave: {
      type: Function
    }
  },
  render(createElement, context) {
    const data = {
      props: {
        name: `expand`,
      },
      on: {
        afterEnter(element) {
          // eslint-disable-next-line no-param-reassign
          element.style.height = `auto`;
          if(context.props.afterEnter) {
            context.props.afterEnter();
          }
        },
        afterLeave(element) {
          // eslint-disable-next-line no-param-reassign
          if(context.props.afterLeave) {
            context.props.afterLeave();
          }
        },
        enter(element) {
          const { width } = getComputedStyle(element);
          /* eslint-disable no-param-reassign */
          element.style.width = width;
          element.style.position = `absolute`;
          element.style.visibility = `hidden`;
          element.style.height = `auto`;
          /* eslint-enable */
          const { height } = getComputedStyle(element);
          /* eslint-disable no-param-reassign */
          element.style.width = "inherit";
          element.style.position = "inherit";
          element.style.visibility = "inherit";
          element.style.height = 0;
          /* eslint-enable */
          // Force repaint to make sure the
          // animation is triggered correctly.
          // eslint-disable-next-line no-unused-expressions
          getComputedStyle(element).height;
          requestAnimationFrame(() => {
            // eslint-disable-next-line no-param-reassign
            element.style.height = height;
          });
        },
        leave(element) {
          const { height } = getComputedStyle(element);
          // eslint-disable-next-line no-param-reassign
          element.style.height = height;
          // Force repaint to make sure the
          // animation is triggered correctly.
          // eslint-disable-next-line no-unused-expressions
          getComputedStyle(element).height;
          requestAnimationFrame(() => {
            // eslint-disable-next-line no-param-reassign
            element.style.height = 0;
          });
        },
      },
    };
    return createElement(`transition`, data, context.children);
  },
};
</script>

<style scoped>
* {
  will-change: height;
  transform: translateZ(0);
  backface-visibility: hidden;
  perspective: 1000px;
}
</style>

<style>
.expand-enter-active,
.expand-leave-active {
  transition: height 1s;
  overflow: hidden;
}
.expand-enter,
.expand-leave-to {
  height: 0;
}
</style>
