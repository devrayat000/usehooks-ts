```tsx

import useIsMounted from './useIsMounted'

const delay = (ms: number) => new Promise(resolve => setTimeout(resolve, ms))

function Child() {
  const [data, setData] = useState('loading')
  const isMounted = useIsMounted()

  // simulate an api call and update state
  useEffect(() => {
    delay(3000).then(() => {
      if (isMounted()) setData('OK')
    })
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, [])

  return <p>{data}</p>
}

export default function Component() {
  const [isVisible, setVisible] = useState<boolean>(false)

  const toggleVisibility = () => setVisible(state => !state)

  return (
    <>
      <button onClick={toggleVisibility}>{isVisible ? 'Hide' : 'Show'}</button>

      {isVisible && <Child />}
    </>
  )
}
```