```javascript

export const ExampleComponent = () => {
  const params = useParams()
  const card = _.get(params, 'nameExample')
  const translate = useTranslate()
  const tenant = useGetTenant()

  const [affiliateId, setAffiliateId] = useState<any>("")

  const onChangeAffiliate = (event: React.ChangeEvent<HTMLInputElement>) => {
    const newAffiliateId = event.target.value.trim()
    if (!newAffiliateId) {
      setAffiliateId(undefined)
    }
    setAffiliateId(newAffiliateId || "")
  }


  useEffect(() => {
  }, [affiliateId])

  return (
    <DataListView
      resource={`${resource}/${card}/`}
      bulkActionButtons={false}
      filters={[
        <TextInput
          alwaysOn
          fullWidth
          source="affiliateId"
          label="This is label"
          onChange={onChangeAffiliate}
          value={affiliateId}
        />
      ]}
      filterDefaultValues={{ affiliateId: "" }}
      cardActions={[<ExportButton />]}
      ignoreCheckTenant={tenant.store ? false : true}
      title={translate('menu.reports.affiliate-order')}
    >
```
