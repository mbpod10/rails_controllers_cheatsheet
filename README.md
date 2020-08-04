## Rails Controllers

# ACTIONS

| CRUD FUNCTION | Rails method |
| ------------- | ------------ |
| GET (all)     | index        |
| POST          | create       |
| GET (by id)   | show         |
| PATCH         | update       |
| PUT           | update       |
| DELETE        | destroy      |

# OVERVIEW

```
class TweetsController < ApplicationController
    def index
        tweets = Tweet.order(:id)
        render json: {status: 200, tweets: tweets}
    end

    def show
        puts "params #{params[:id]}"
        tweet = Tweet.find(params[:id])
        render json: {status: 200, tweet: tweet}
    end

    def create
        tweet = Tweet.new(tweet_params)
        if tweet.save
            render(status: 201, json: { status: 201, tweet: tweet })
          else
            render(status: 422, json: { status: 422, tweet: tweet })
          end
    end

    def update
        tweet = Tweet.find(params[:id])
        tweet.update(tweet_params)
        render(status: 201, json: { status: 201, tweet: tweet })
    end

    def destroy
        tweet = Tweet.destroy(params[:id])
        render(status: 201, json: { status: 201, tweet: tweet })
    end

    private
    def tweet_params
        params.required(:tweet).permit(:title, :content, :author)
    end

end
```
