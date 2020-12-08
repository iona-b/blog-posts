![Cover Image](./cover-image.jpg)

*photo by [@estudiobloom](https://unsplash.com/@estudiobloom)*

# RSpec and Rails

## 1. Install Rails RSpec

1. gem 'rspec-rails', '~> 3.4', '>= 3.4.2' in group :development, :test do
2. bundle install
3. rails generate rspec:install

What files does this create?

## 2. Create an Instance to Test

```ruby
before(:all) do
    @song = Song.create(title: "Like a Rolling Stone", artist: "Bob Dylan", album:"Highway 61 Revisited", release_date: 1965)
end
```

![Pomegranate](./pomegranate.jpg)

*photo by [@matyszczyk](https://unsplash.com/@matyszczyk)*

## 3. Create Your CRUD Tests

### Create

```ruby
it 'checks that a song can be created' do
    expect(@song).to be_valid
end
```

### Read

```ruby
it 'checks that a song can be created' do
    expect(Song.find_by_title("Like a Rolling Stone")).to eq(@song)
end
```

### Edit

```ruby
it 'checks that a song can be created' do
    @song.update(:title => "Like a Rolling Stone - Remastered")
    expect(Song.find_by_title("Like a Rolling Stone - Remastered")).to eq(@song)
end
```

### Delete

```ruby
it 'checks that a song can be created' do
    @song.destroy
    expect(Song.count).to eq(0)
end
```

## Sources

1. "[rspec-rails](https://rubygems.org/gems/rspec-rails/versions/3.4.2)", rubygems.org, Accessed December 7, 2020
2. "[TDD Basics: How to Write an RSpec Test](https://dev.to/jeremy/rspec-from-scratch-part-1-how-to-write-a-test-4ce8)", Jeremy Schuurmans on DEV, Accessed December 7, 2020