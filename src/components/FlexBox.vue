<script lang="jsx" setup>
import { defineProps, getCurrentInstance } from 'vue'

const _self = getCurrentInstance()
const props = defineProps({
  classList: Array
})

_self.render = () => (
  <div className={`boxWrapper d-flex ${props.classList.join(' ')}`}>
    {Array.from({ length: 10 }).map((item, key) =>
      <div className="boxItem" key={key}>{ key + 1 }</div>
    )}
  </div>
)
</script>
