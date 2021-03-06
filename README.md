# motion-stylez (z)

A super basic RubyMotion stylesheet library based off Todd Werth's [RMQ library](https://github.com/infinitered/rmq) that lets you centralize your view styles.

## Help support this gem by learning

The only reason I can keep making gems and keep them up to date is because lovely people like yourself support me. I run the [MotionInMotion screencasts](https://motioninmotion.tv/) which you can sign up to for $9/month, I also have a book coming out called [RubyMotion for Rails Developers](http://book.motioninmotion.tv/) which you can pay what you like to buy, and I provide one-on-one training through pairing on [AirPair{}Me](http://airpair.me/fluffyjack?utm_source=expert&utm_medium=readme&utm_term=motion-stylez&utm_content=github&utm_campaign=airpairme). All support, even small amounts really helps.

## Installation

Add this line to your application's Gemfile:

    gem 'motion-stylez'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install motion-stylez

## Usage

You can use the `z` method from anywhere in your application.

First you will need to set your stylesheet.

```ruby
z.stylesheet = MyStylesheet.new
```

Then create your stylesheet and it's styles.

```ruby
class MyStylesheet
  def bw_big(v)
    v.backgroundColor = UIColor.blackColor
    v.textColor = UIColor.whiteColor
    v.font = UIFont.systemFontOfSize(36)
    v.frame = [[20, 40], [280, 50]]
    v.textAlignment = UITextAlignmentCenter
  end

  def white_bg(v)
    v.backgroundColor = UIColor.whiteColor
  end

  def blue_bg(v)
    v.backgroundColor = UIColor.blueColor
  end
end
```

Then you can use the `z` method to create your styled view, which you can also pass a block to. For example, use in a controller.

```ruby
class MyViewController < UIViewController
  def viewDidLoad
    super
 
    z.stylesheet = MyStylesheet.new # works absolutely anywhere
 
    z(self.view, :white_bg)
 
    self.view.addSubview(z(UILabel, :bw_big) do |v|
      v.text = ":bw_big"
      v.frame = [[20, 40], [280, 50]]
    end)

    # OR YOU CAN DO THE LONG WAY
    # z(self.view).style(:white_bg)
    #
    # self.view.addSubview(z(UILabel).style(:bw_big) do |v|
    #   v.text = "Testing"
    # end)

    self.view.addSubview(z(UILabel, [:bw_big, :blue_bg]) do |v|
      v.text = ":bw_big & :blue_bg"
      v.frame = [[20, 100], [280, 50]]
    end)

    self.view.addSubview(UILabel.new.style([:bw_big, :blue_bg]) do |v|
      v.text = "alt sytax 1"
      v.frame = [[20, 160], [280, 50]]
    end)

    self.view.addSubview(UILabel.style([:bw_big, :blue_bg]) do |v|
      v.text = "alt sytax 2"
      v.frame = [[20, 220], [280, 50]]
    end)
 
  end
end
```

## Contributing

1. Fork it ( http://github.com/FluffyJack/motion-stylez/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
