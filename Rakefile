require 'json'
require 'net/http'
require 'twitter'

task :run do
  json = Net::HTTP.get(URI('https://feeds.pinboard.in/json/popular'))
  ids = JSON.parse(json).map { |item| item['u'].match(%r{twitter.com/.+/status/(\d+)}) }.compact.map { |match| match[1].to_i }

  client = Twitter::REST::Client.new do |config|
    config.consumer_key = ENV['CONSUMER_KEY']
    config.consumer_secret = ENV['CONSUMER_SECRET']

    # @PinPopularRTs
    config.access_token = ENV['ACCESS_TOKEN']
    config.access_token_secret = ENV['ACCESS_TOKEN_SECRET']
  end

  ids.map { |id| client.retweet(id) }
end
