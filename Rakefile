# encoding: utf-8

ROOT_DIR = File.dirname(__FILE__)

desc 'Begin a new post'
task :post, :title do |t, args|
  args.with_defaults(title: 'new-post')
  title = args.title
  slug = title.strip.downcase.gsub(/ /, '-')
  filename = "#{ROOT_DIR}/_posts/#{Time.now.strftime('%Y-%m-%d')}-#{slug}.md"
  File.open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "title: \"#{title.gsub(/&/,'&amp;')}\""
    post.puts "date: #{Time.now.strftime('%Y-%m-%d %H:%M')}"
    post.puts "comments: true"
    post.puts "---"
    post.puts "Kisa aciklama..."
    post.puts "<!-- more -->"
  end
  system("vim", filename)
end
