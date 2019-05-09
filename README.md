# twitter_batch
TwitterのREST APIを定期実行してbotのmentionに逐次対応するgemを作る

## 思想
```ruby
require 'twitter'
require 'twitter_batch'

client = Twitter::REST::Client.new do |config|
  config.consumer_key        = ENV["MY_CONSUMER_KEY"]
  config.consumer_secret     = ENV["MY_CONSUMER_SECRET"]
  config.access_token        = ENV["MY_ACCESS_TOKEN"]
  config.access_token_secret = ENV["MY_ACCESS_TOKEN_SECRET"]
end

mention_batch = TwitterBatch::Mention.new do |config|
  config.client = client
  config.dir = './tmp'
end

mention_batch.get(option).each do |tweet|
  tweet.(メンションに実行したい処理)
end
```