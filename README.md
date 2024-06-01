''' コラムの名称変更'''
spot=spot.rename(columns={'受渡日':'Date','時刻コード':'Time','売り入札量(kWh)':'OfferVolume',
                          '買い入札量(kWh)':'BidVolume','約定総量(kWh)':'TradeVolume',
                          'システムプライス(円/kWh)':'SystemPrice','エリアプライス北海道(円/kWh)':'HokkaidoPrice',
                          'エリアプライス東北(円/kWh)':'TohokuPrice','エリアプライス東京(円/kWh)':'TokyoPrice',
                          'エリアプライス中部(円/kWh)':'ChubuPrice','エリアプライス北陸(円/kWh)':'HokurikuPrice',
                          'エリアプライス関西(円/kWh)':'KansaiPrice','エリアプライス中国(円/kWh)':'ChugokuPrice',
                          'エリアプライス四国(円/kWh)':'ShikokuPrice','エリアプライス九州(円/kWh)':'KyushuPrice',
                          '売りブロック入札総量(kWh)':'OfferBlockVolume',
                          '売りブロック約定総量(kWh)':'OfferBlockTradeVolume',
                          '買いブロック入札総量(kWh)':'BidBlockVolume',
                          '買いブロック約定総量(kWh)':'BidBlockTradeVolume'})
''' ソート用日付コラム追加'''

spot['Date']=pd.to_datetime(spot['Date'])
spot['Year']=spot['Date'].dt.year
spot['Month']=spot['Date'].dt.month
spot['WeekNum']=spot['Date'].dt.week
spot['Weekday']=spot['Date'].dt.weekday
spot['Day']=spot['Date'].dt.day

holiday['Date']=pd.to_datetime(holiday['Date'])
for i in holiday['Date']:
    spot["Weekday"].mask(holiday["Date"] == i, 7, inplace=True)                      
