# RPPOON_LV1_RALASIC
Program.cs
namespace lv1_ralasic
{
    
    class Program
    {
        static void Main(string[] args)
        {
            
            /*Note noteOne = new Note("Ivan");
            Note noteTwo = new Note("Pero", "Treci zadatak");
            Note noteThree = new Note("Jakov", "Drugi zadatak", 3);*/
            ToDo list;
            list = new ToDo();
            TimeNote time_note_1, time_note_2, time_note_3;
            time_note_1 = new TimeNote(DateTime.Now, "Ivan", "Prvi zadatak", 0);
            time_note_2 = new TimeNote(DateTime.Now, "Pero", "Drugi zadatak!", 1);
            time_note_3 = new TimeNote(DateTime.Now, "Jakov", "Treci zadatak!", 2);
            list.AddNote(time_note_1);
            list.AddNote(time_note_2);
            list.AddNote(time_note_3);
            list.Sort();
            Console.WriteLine(list.NotesToString());

            list.CompletingNote();
            Console.WriteLine(list.NotesToString());
        }
    }


Note.cs


    class Note
    {
        private String task;
        private String author;
        private int priority;
        public string Task
        {
            get { return this.task; }
            set { this.task = value; }
        }
        public int Priority
        {
            get { return this.priority; }
            set
            {
                if (value > 5 || value < 1)
                {
                    this.priority = 0;
                }
                else
                {
                    this.priority = value;
                }
            }
        }
        public string Author
        {
            get { return this.author; }
        }
        
        public Note(String author, String task,int priority)
        {
            this.author = author;
            this.task = task;
            this.priority = priority;
        }
        public Note(String author, String task)
        {
            this.author = author;
            this.task = task;
            this.priority = 0;
        }
        public Note(String author)
        {
            this.author = author;
            this.task = "dodaj kasnije";
            this.priority = 0;
        }
        public override string ToString()
        {
            return "Author: " + this.author + "\nTask: " + this.task + "\nPriority: " + this.priority + "\n";
        }

        public int CompareTo(INote note)
        {
            return this.Priority.CompareTo(note.Priority);
        }
    }


ToDo.cs

class ToDo
    {
        List<TimeNote> notes;
        public ToDo()
        {
            notes = new List<TimeNote>();
        }
        public void AddNote(TimeNote note)
        {
            notes.Add(note);
        }
        public String NotesToString()
        {
            StringBuilder stringBuilder = new StringBuilder();
            foreach (TimeNote note in notes)
            {
                stringBuilder.Append(note).Append("\n");
            }
            return stringBuilder.ToString();

        }
        public void Sort()
        {
            notes.Sort();
        }

        public void CompletingNote()
        {
            for (int i = 0; i < notes.Count; i++)
            {
                if (notes[i].Priority == 1)
                {
                    notes.RemoveAt(i);
                    i--;
                }
            }
        }
    }


TimeNote.cs
class TimeNote:Note, IComparable<TimeNote>
    {
        private DateTime time;
        public TimeNote (DateTime time, string author, string task, int priority):base (author,task,priority)
        {
            this.time = time; 
        }
        public DateTime Time
        {
            get { return this.time; }
            set { this.time = value; }
        }
        public override string ToString()
        {
            return base.ToString() + this.time + "\n";
        }
        public int CompareTo(TimeNote note)
        {
            return this.Priority.CompareTo(note.Priority);
        }
    }


INote.cs

interface INote: IComparable<INote>
    {
        string Task
        {
            get;
            set;
        }
        string Author
        {
            get;
        }
        int Priority
        {
            get;
            set;
        }

        int CompareTo(INote note);
    }
