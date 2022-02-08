<script>
  export default {
    name: 'PageLayout',
  
    functional: true,
  
    props: {
      
    },
  
    computed: {
      name () {
        return `fade-slide-${this.direction}`
      },
  
      component () {
        return this.group ? 'transition-group' : 'transition'
      },
    },
  
    render (h, { props, children }) {
      return h(
        props.group ? 'TransitionGroup' : 'Transition',
        {
          props: {
            name: `fade-slide-${props.direction}`,
            ...props,
          },
        },
        children,
      )
    },
  }
  </script>
  
<style lang="stylus">
</style>
  