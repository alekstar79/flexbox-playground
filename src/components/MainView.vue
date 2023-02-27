<script lang="jsx" setup>
import { getCurrentInstance, reactive } from 'vue'

import ItemSelector from '@/components/ItemSelector'
import RadioBtn from '@/components/RadioBtn'
import FlexItem from '@/components/FlexItem'
import FlexBox from '@/components/FlexBox'

const state = reactive({
  dirList: [
    { text: 'row', class: '' },
    { text: 'column', class: 'flex-column' },
    { text: 'row-reverse', class: 'flex-row-reverse' },
    { text: 'column-reverse', class: 'flex-column-reverse' }
  ],
  wrapList: [
    { text: 'nowrap', class: '' },
    { text: 'wrap', class: 'flex-wrap' },
    { text: 'wrap-reverse', class: 'flex-wrap-reverse' }
  ],
  jcList: [
    { text: 'flex-start', class: '' },
    { text: 'flex-end', class: 'justify-content-end' },
    { text: 'center', class: 'justify-content-center' },
    { text: 'space-between', class: 'justify-content-between' },
    { text: 'space-around', class: 'justify-content-around' }
  ],
  aiList: [
    { text: 'flex-start', class: '' },
    { text: 'flex-end', class: 'align-items-end' },
    { text: 'center', class: 'align-items-center' },
    { text: 'baseline', class: 'align-items-baseline' },
    { text: 'stretch', class: 'align-items-stretch' }
  ],
  acList: [
    { text: 'flex-start', class: '' },
    { text: 'flex-end', class: 'align-content-end' },
    { text: 'center', class: 'align-content-center' },
    { text: 'space-between', class: 'align-content-between' },
    { text: 'space-around', class: 'align-content-around' },
    { text: 'stretch', class: 'align-content-stretch' }
  ],
  // flex container
  containerVal: {
    dirVal: 0,    // flex-direction
    wrapVal: 0,   // flex-wrap
    jcVal: 0,     // justify-content
    aiVal: 0,     // align-items
    acVal: 0,     // align-content
  },
  // flex items
  itemVal: [
    { grow: 0, shrink: 1, basis: 0, order: 0, self: 0 },
    { grow: 0, shrink: 1, basis: 0, order: 0, self: 0 },
    { grow: 0, shrink: 1, basis: 0, order: 0, self: 0 },
    { grow: 0, shrink: 1, basis: 0, order: 0, self: 0 },
    { grow: 0, shrink: 1, basis: 0, order: 0, self: 0 }
  ],
  asList: [
    { text: 'auto', class: '' },
    { text: 'flex-start', class: 'align-self-start' },
    { text: 'flex-end', class: 'align-self-end' },
    { text: 'center', class: 'align-self-center' },
    { text: 'baseline', class: 'align-self-baseline' },
    { text: 'stretch', class: 'align-self-stretch' }
  ],
  fbList: [
    { text: 'auto', class: '' },
    { text: '0px', class: 'flex-basis-0' },
    { text: '100px', class: 'flex-basis-px' },
    { text: '50%', class: 'flex-basis-percent' },
  ]
})

const setConVal = (attr, val) => {
  const newVal = { ...state.containerVal }

  newVal[attr] = Number(val)

  state.containerVal = newVal
}

const setItemVal = (index, attr, val) => {
  const newVal = state.itemVal.map(item => ({ ...item }))

  newVal[index][attr] = Number(val)

  state.itemVal = newVal
}

const setClass = () => {
  const { containerVal } = state

  const convertList = {
    dirVal: 'dirList',
    wrapVal: 'wrapList',
    jcVal: 'jcList',
    aiVal: 'aiList',
    acVal: 'acList',
  }

  return Object.keys(containerVal)
    .reduce((pre, el) => {
      if (!!containerVal[el] && convertList[el]) {
        const attrList = state[convertList[el]]

        return pre.concat(attrList[containerVal[el]].class)
      } else {
        return pre
      }
    }, [])
}

const initCon = () => {
  const newVal = { ...state.containerVal }

  Object.keys(newVal).map(item => newVal[item] = 0)

  state.containerVal = newVal
}

const initItems = () => {
  state.itemVal = Array.from({length: 5}, () => ({
    grow: 0, shrink: 1, basis: 0, order: 0, self: 0
  }))
}

const radioContent = (title, btnName, list, valName) => (
  <div className="mb-2 row align-items-center">
    <span className="col-lg-2 mb-lg-0 mb-1 font-weight-bold">
      {title}
    </span>

    <div className="col-lg-10">
      <RadioBtn
        name={btnName}
        list={list}
        value={state.containerVal[valName]}
        onChange={e => setConVal(valName, e.target.value)}
      />
    </div>
  </div>
)

const _self = getCurrentInstance()

_self.render = () => (
  <div className="container pt-2 pb-5">
    <h1 className="text-center mb-4">Flexbox Playground</h1>

    <h3 className="my-4">
      <span role="img">🧀</span> flex container
      <button className="btn btn-sm btn-outline-danger ml-4" onClick={initCon}>
        reset
      </button>
    </h3>

    {radioContent('flex-direction', 'dirBtn', state.dirList, 'dirVal')}
    {radioContent('flex-wrap', 'wrapBtn', state.wrapList, 'wrapVal')}
    {radioContent('justify-content', 'jcBtn', state.jcList, 'jcVal')}
    {radioContent('align-items', 'aiBtn', state.aiList, 'aiVal')}
    {radioContent('align-content', 'acBtn', state.acList, 'acVal')}

    {!!state.containerVal.acVal && !state.containerVal.wrapVal &&
      <div className="text-danger">* ALIGN-CONTENT need to use with WRAP!!</div>
    }

    <FlexBox classList={setClass()} />

    <h3 className="my-4">
      <span role="img">🧀</span> flex items
      <button className="btn btn-sm btn-outline-danger ml-4" onClick={initItems}>
        reset
      </button>
    </h3>

    <div className="selectorWrapper">
      {Array.apply(null, Array(5)).map((item, key) =>
        <ItemSelector
          setItemVal={(attr, val) => setItemVal(key, attr, val)}
          params={state.itemVal[key]}
          asList={state.asList}
          fbList={state.fbList}
          number={key + 1}
          key={key}
        />
      )}
    </div>

    <FlexItem
      itemVal={state.itemVal}
      asList={state.asList}
      fbList={state.fbList}
    />
  </div>
)
</script>
