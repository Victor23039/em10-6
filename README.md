using System.Text;

namespace ConsoleApp50
{

    class Blog
    {
        private List<Article> Articles { get; set; }

        public Blog()
        {
            Articles = new List<Article>();
        }

        public void AddArticle(Article article)
        {
            Articles.Add(article);
        }

        public List<Article> GetAllArticles()
        {
            return Articles;
        }

        public Article GetArticleById(int id)
        {
            return Articles.First(article => article.Id == id);
        }
    }

    class Article
    {
        public int Id { get; set; }
        public string Title { get; set; }
        public string Text { get; set; }
        public User CreatedBy { get; set; }
        public List<Comment> Comments { get; set; }


        public Article(string title, string text, User createdBy)
        {
            Id++;
            this.Title = title;
            this.Text = text;
            this.CreatedBy = createdBy;
            this.Comments = new List<Comment>();
        }

        public void Edit(string title, string text)
        {
            Title = title;
            Text = text;
        }

        public void Delete()
        {
            Title = null;
            Text = null;
            CreatedBy = null;
            Comments = null;
        }

        public void AddComment(Comment comment)
        {
            Comments.Add(comment);
        }

        public List<Comment> GetAllComments()
        {
            return Comments;
        }
    }

    class User
    {
        public string Email { get; set; }
        public string Password { get; set; }

        public User(string email, string password)
        {
            this.Email = email;
            this.Password = password;
        }
    }

    class Comment
    {
        public string Text { get; set; }
        public User CreatedBy { get; set; }
        public int Rating { get; set; }

        public Comment(string text, User createdBy, int rating)
        {
            this.Text = text;
            this.CreatedBy = createdBy;
            this.Rating = rating;
        }
    }

    internal class Program
    {
        static void Main(string[] args)
        {
            Console.OutputEncoding = Encoding.Unicode;
            Console.InputEncoding = Encoding.Unicode;
            User user1 = new User("vasyliy777@gmail.com", "*******");
            User user2 = new User("ivan.blaznov2.com", "************");

            Blog blog = new Blog();

            Article article1 = new Article("Моє життя", "Життя прекрасне!", user1);
            blog.AddArticle(article1);


            Comment comment1 = new Comment("Позитивненько!", user2, 5);
            article1.AddComment(comment1);


            List<Article> allArticles = blog.GetAllArticles();
            foreach (var article in allArticles)
            {
                Console.WriteLine($"Yfpdf cnfnns: {article.Id}-- " +
                    $"'{article.Title}'          " +
                    $"Текст статті: {article.Text}             " +
                    $"Створенно: {article.CreatedBy.Email}");
            }

            Console.WriteLine("Комментарі до статті:");

            List<Comment> allcomments = article1.GetAllComments();
            foreach (var comment in allcomments)
            {
                Console.WriteLine($"{comment.Text}         " +
                    $"Створенно: {comment.CreatedBy}       " +
                    $"{comment.Rating}/5");
            }
        }
    }
}
