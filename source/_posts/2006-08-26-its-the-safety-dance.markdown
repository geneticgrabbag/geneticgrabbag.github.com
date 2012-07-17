---
layout: post
title: "It's the Safety Dance!"
date: 2006-08-26 19:53:40
categories:
- personal
- computing
- software-development
---
Well, my cousin threw down the gaunlet by proposing this quite humorous
programmatic rendition of
[Sir Mix-a-Lot](http://en.wikipedia.org/wiki/Sir_Mix-a-lot)'s indominatable
["I Like Big Butts"](http://www.lyrics007.com/Sir%20Mix-A-Lot%20Lyrics/I%20Like%20Big%20Butts%20Lyrics.html):

``` c#
I.like(bigButts) && I.canLie(false);
otherBrothers.canDeny(false);
when (girl.walksIn())
{
  if (girl.hasIttyBittyWaist() && roundThing.getLocation()==your.FACE)
  {
    you.getSprung();
  }
}
```

{% pullquote %}
Which I thought was quite clever.  So, {"I felt I owed him a response"}
comensurate with the length of time I made him wait for a reply.
{% endpullquote %}

<!--more-->
So, I began thinking for an appropriate song.  Then I remembered
[Men Without Hats](http://en.wikipedia.org/wiki/Men_without_hats)' 1983 classic
["Safety Dance"](http://www.lyricsondemand.com/onehitwonders/safetydancelyrics.html)
and how it contained a lot of if/then and boolean language
("'Cause your friends don't dance and if they don't dance..." etc.).

Here's the program's output that prints the song's lyrics.

{% codeblock Output %}
=================
Men Without Hats
 Safety Dance!
----------------

S-s-s-s A-a-a-a F-f-f-f E-e-e-e T-t-t-t Y-y-y-y
We can dance if we want to
We can leave your friends behind
'Cause your friends don't dance...
...and if they don't dance
Well they're no friends of mine
I say, we can go where we want to
A place where they will never find
And we can act like we come from out of this world
Leave the real one far behind.
And we can dance.
{% endcodeblock %}

And here's the program's output with log statement enabled.
Show's the program's hilarious logic.

{% codeblock Output with Logging %}
=================
Men Without Hats
 Safety Dance!
----------------

>> Created a new person with name Evan.
>> Created us.
>> Created a new person with name J.B..
>> Created a new person with name JoeDoc.
>> Created a new person with name Clio.
>> Created them.
>> Created a new person with name Shrub.
>> Created a new person with name Rummy.
>> Created a new person with name Cheney.
>> Created a new person with name Karl Rove.
>> Created Separation Group #1.
>> Created Separation Group #2.
>> Created Separation Group #3.
>> Created Separation Group #4.
>> Created Separation Group #5.
>> Created Separation Group #6.
>> Created Separation Group #7.
>> Created Separation Group #8.
>> Created Separation Group #9.
S-s-s-s A-a-a-a F-f-f-f E-e-e-e T-t-t-t Y-y-y-y
We can dance if we want to
>> Evan can now dance.
>> J.B. can now dance.
>> JoeDoc can now dance.
>> Clio can now dance.
>> We and they have a separation of -10 spots (FarBehind).
>> Can we leave them far behind: True
We can leave your friends behind
'Cause your friends don't dance...
>> Shrub can no longer dance.
>> Rummy can no longer dance.
>> Cheney can no longer dance.
...and if they don't dance
Well they're no friends of mine
>> Removing those friends of Evan who cannot dance
>> Shrub is not a friend of Evan; no need to remove.
>> Rummy is not a friend of Evan; no need to remove.
>> Cheney is not a friend of Evan; no need to remove.
I say, we can go where we want to
>> Evan can now go to WhereWeWantTo.
>> J.B. can now go to WhereWeWantTo.
>> JoeDoc can now go to WhereWeWantTo.
>> Clio can now go to WhereWeWantTo.
A place where they will never find
>> They cannot find us.
And we can act like we come from out of this world
>> Evan is acting like earth is not his/her place of origin.
>> J.B. is acting like earth is not his/her place of origin.
>> JoeDoc is acting like earth is not his/her place of origin.
>> Clio is acting like earth is not his/her place of origin.
Leave the real one far behind.
>> Evan is leaving the real world far behind.
>> J.B. is leaving the real world far behind.
>> JoeDoc is leaving the real world far behind.
>> Clio is leaving the real world far behind.
And we can dance.
>> Evan can now dance.
>> J.B. can now dance.
>> JoeDoc can now dance.
>> Clio can now dance.
{% endcodeblock %}

Here's a link to the Windows Microsoft.Net executable:

[SafetyDance.exe](/images/2006/08/SafetyDance.exe)

{% codeblock MD5 Checksum %}
5A5ECE6B9A5984AACDE5564440BA7A66 SafetyDance.exe
{% endcodeblock %}

And, finally, here's the C# source code:

{% codeblock lang:csharp Source Code %}
using System;
using System.Collections;
using System.Collections.Specialized;
using System.Text;
/*
using Imagination;
using Inanity;
using Youth;
using Relatives.Aunts.Barbara;
 */

namespace Dance.Safety
{

    /// <summary>
    ///        Classes for simulating the "Safety Dance" song by the
    ///        group Men Without Hats.
    /// </summary>
    /// <remarks>
    ///     Date            Author          Action
    ///     =============   =============   =====================
    ///        2006-Aug-26     Evan P. Mills   Initial release.
    ///
    ///        Lyrics courtesy Lyrics(On)Demand:
    ///            http://www.lyricsondemand.com/onehitwonders/safetydancelyrics.html
    ///
    ///     This work is licensed under a Creative Commons Attribution-NonCommercial-NoDerivs 2.5
    ///     License. See http://creativecommons.org/licenses/by-nc-nd/2.5/.
    ///    </remarks>
    public class NamespaceDoc
    {
    }


    /// <summary>
    ///        Class that processes the song "Safety Dance".
    /// </summary>
    public class SafetyDance
    {
        /// <summary>
        ///     S-s-s-s  A-a-a-a  F-f-f-f T-t-t-t  Y-y-y-y
        /// </summary>
        protected const string SAFETY_WORD = "safety";


        /// <summary>
        ///        A list of locations mentioned in the song.
        /// </summary>
        protected enum Location
        {
            Nowhere,
            Behind,
            OutOfThisWorld,
            WhereWeWantTo
        }

        /// <summary>
        ///     Relative linear positions.
        /// </summary>
        public enum RelativeLinearPosition
        {
            Incomparable,
            FarBehind,
            CloseBehind,
            CloseAhead,
            FarAhead
        }

        /// <summary>
        ///     How much does a person want to perform an act?
        /// </summary>
        public enum Desire
        {
            GodNo,
            NotReally,
            TakeItOrLeaveIt,
            Somewhat,
            YouBet
        }

        /// <summary>
        ///        A function or method that simulates behavior.
        /// </summary>
        public delegate void BehaviorDelegate();


        /// <summary>
        ///     Compares distances.
        /// </summary>
        public class DistanceComparator
        {
            static internal int THRESH_FAR_BEHIND = -10;
            static internal int THRESH_CLOSE_BEHIND = -3;
            static internal int THRESH_CLOSE_AHEAD = +3;
            static internal int THRESH_FAR_AHEAD = +10;

            /// <summary>
            ///     Returns a relative linear position for a given
            ///     distance.
            /// </summary>
            static public RelativeLinearPosition FromDistance(int distance)
            {
                if (distance <= THRESH_FAR_BEHIND)
                    return RelativeLinearPosition.FarBehind;
                else if (distance <= THRESH_CLOSE_BEHIND)
                    return RelativeLinearPosition.CloseBehind;
                else if (distance <= THRESH_CLOSE_AHEAD)
                    return RelativeLinearPosition.CloseAhead;
                else
                    return RelativeLinearPosition.FarAhead;
            }
        }

        /// <summary>
        ///        A person.
        /// </summary>
        protected class Person
        {
            // Public Properties:
            public string Name = null;
            private bool m_canDance = true;
            private Desire m_danceDesire = Desire.TakeItOrLeaveIt;
            private Hashtable m_canGo = new Hashtable();
            private Hashtable m_canFind = new Hashtable();
            public PersonCollection Friends = null;


            /// <summary>
            ///        Cannot create a person without a name.
            ///    </summary>
            private Person() { }

            /// <summary>
            ///        Creates a new person with the given name.
            ///    </summary>
            public Person(string name)
            {
                this.Name = name;
                Log("Created a new person with name {0}.", name);

                string groupName = "Friends of " + this.Name;
                // this.Friends = new PersonCollection(groupName, groupName);
            }

            /// <summary>
            ///     Returns true if this person can dance.
            /// </summary>
            public bool CanDance
            {
                get { return m_canDance; }
                set
                {
                    m_canDance = value;
                    Log("{0} {1} dance.",
                        this.Name,
                        value ? "can now" : "can no longer"
                        );
                }
            }

            /// <summary>
            ///     Returns the relative desire this person has to dance.
            /// </summary>
            public Desire DanceDesire
            {
                get { return m_danceDesire; }
                set
                {
                    m_danceDesire = value;
                    Log("{0} now views dancing as {1}.", Name, value.ToString());
                }
            }

            /// <summary>
            ///     Returns true if this person wants to dance.
            /// </summary>
            public bool WantToDance
            {
                get
                {
                    bool result = ((int)m_danceDesire > (int)Desire.NotReally);
                    Log("{0} {1} to dance ({2}).",
                        this.Name,
                        result ? "wants" : "does not want",
                        this.DanceDesire
                    );
                    return result;
                }
            }

            /// <summary>
            ///     Makes this person dance.
            /// </summary>
            public void Dance()
            {
                if (WantToDance == false)
                {
                    Log("{0} doesn't want to dance!", Name);
                    return;
                }
                Log("{0} views dancing as: {1}", Name, DanceDesire);
                Log("{0} has danced.", Name);
            }

            /// <summary>
            ///     Sets whether this person can go to the given location.
            /// </summary>
            /// <param name="location">
            ///     The location of interest.
            /// </param>
            /// <param name="canGo">
            ///     True if this person can go to this location; false, otherwise.
            /// </param>
            public void SetCanGo(Location location, bool canGo)
            {
                m_canGo[location.ToString()] = true;
                Log("{0} {1} go to {2}.",
                    this.Name,
                    canGo ? "can now" : "can lo longer",
                    location
                );
            }

            /// <summary>
            ///     Returns whether this person can go to the give location.
            /// </summary>
            /// <param name="location">
            ///     The location of interest.
            /// </param>
            /// <returns>
            ///     True if this person can go to the given location.
            /// </returns>
            public bool CanGo(Location location)
            {
                return m_canGo.Contains(location.ToString());
            }

            /// <summary>
            ///     Sets whether this person can find the given location.
            /// </summary>
            /// <param name="location">
            ///     The location of interest.
            /// </param>
            /// <param name="canFind">
            ///     True if this person can find this location; false, otherwise.
            /// </param>
            public void SetCanFind(Location location, bool canFind)
            {
                m_canFind[location.ToString()] = true;
                Log("{0} {1} find {2}.",
                    this.Name,
                    canFind ? "can now" : "can lo longer",
                    location
                );
            }

            /// <summary>
            ///     Returns whether this person find the give location.
            /// </summary>
            /// <param name="location">
            ///     The location of interest.
            /// </param>
            /// <returns>
            ///     True if this person can find the given location.
            /// </returns>
            public bool CanFind(Location location)
            {
                return m_canFind.Contains(location.ToString());
            }

            /// <summary>
            ///     Makes this person perform an action.
            /// </summary>
            /// <param name="behavior">
            ///     The behavior to perform.
            /// </param>
            public void Act(BehaviorDelegate behavior)
            {
                behavior();
            }

            /// <summary>
            ///     Makes a person act like he/she comes from
            ///     out of this world.
            /// </summary>
            public void ActLikeWeComeFromOutOfThisWorld()
            {
                Log("{0} is acting like earth is not his/her place of origin.",
                    this.Name
                );
            }

            /// <summary>
            ///     Makes the person leave this world behind.
            /// </summary>
            public void LeaveTheRealWorldFarBehind()
            {
                Log("{0} is leaving the real world far behind.", this.Name);
            }

        }


        /// <summary>
        ///        A collection of people (e.g. a group).
        /// </summary>
        protected class PersonCollection : ArrayList
        {
            private string m_nameAsSubject = null;
            private string m_nameAsObject = null;


            /// <summary>
            ///     Creates a new collection of people.
            /// </summary>
            /// <param name="nameAsSubject">
            ///     How one refers to this group as the subject of
            ///     an action.
            /// </param>
            /// <param name="nameAsObject">
            ///     How one refers to this group as the object of
            ///     an action.
            /// </param>
            public PersonCollection(string nameAsSubject, string nameAsObject)
                : base()
            {
                m_nameAsSubject = nameAsSubject;
                Log("Created {0}.", nameAsObject);
            }

            /// <summary>
            ///     Gets or sets this group's name as a subject.
            /// </summary>
            public string NameAsSubject
            {
                get { return m_nameAsSubject; }
                set { m_nameAsSubject = value; }
            }

            /// <summary>
            ///     Gets or sets this group's name as an object.
            /// </summary>
            public string NameAsObject
            {
                get { return m_nameAsObject; }
                set { m_nameAsObject = value; }
            }

            /// <summary>
            ///     Returns true if the group can collectively dance.
            /// </summary>
            /// <remarks>
            ///     The group can dance if and only if if all its
            ///     members can dance.
            /// </remarks>
            public bool CanDance
            {
                get
                {
                    Object[] persons = this.ToArray();
                    Person person;

                    for (int i = persons.GetLowerBound(0); i <= persons.GetUpperBound(0); i++)
                    {
                        person = persons[i] as Person;
                        if (person.CanDance == false)
                            return false;
                    }

                    return true;
                }
                set
                {
                    Object[] persons = this.ToArray();
                    Person person;

                    for (int i = persons.GetLowerBound(0); i <= persons.GetUpperBound(0); i++)
                    {
                        person = persons[i] as Person;
                        person.CanDance = value;
                    }
                }
            }

            /// <summary>
            ///     Makes the people of this group dance.
            /// </summary>
            public void Dance()
            {
                Object[] persons = this.ToArray();
                Person person;

                for (int i = persons.GetLowerBound(0); i <= persons.GetUpperBound(0); i++)
                {
                    person = persons[i] as Person;
                    person.Dance();
                }
            }

            public void SetCanGo(Location location, bool canGo)
            {
                Object[] persons = this.ToArray();
                Person person;

                for (int i = persons.GetLowerBound(0); i <= persons.GetUpperBound(0); i++)
                {
                    person = persons[i] as Person;
                    person.SetCanGo(location, canGo);
                }
            }

            public bool CanFind(Location location)
            {
                Object[] persons = this.ToArray();
                Person person;

                for (int i = persons.GetLowerBound(0); i <= persons.GetUpperBound(0); i++)
                {
                    person = persons[i] as Person;
                    if (person.CanFind(location))
                        return true;
                }

                return false;
            }

            public void ActLikeWeComeFromOutOfThisWorld()
            {
                Object[] persons = this.ToArray();
                Person person;

                for (int i = persons.GetLowerBound(0); i <= persons.GetUpperBound(0); i++)
                {
                    person = persons[i] as Person;
                    person.Act(new BehaviorDelegate(person.ActLikeWeComeFromOutOfThisWorld));
                }
            }

            public void LeaveTheRealWorldFarBehind()
            {
                Object[] persons = this.ToArray();
                Person person;

                for (int i = persons.GetLowerBound(0); i <= persons.GetUpperBound(0); i++)
                {
                    person = persons[i] as Person;
                    person.LeaveTheRealWorldFarBehind();
                }
            }

        }

        protected class GroupQueue : Queue
        {
            const int BIG_SEPARATION = 10;


            public GroupQueue()
                : base()
            {
            }

            public RelativeLinearPosition RelativePosition (PersonCollection group1, PersonCollection group2)
            {
                int pos1 = GetPosition(group1);
                int pos2 = GetPosition(group2);

                RelativeLinearPosition result = DistanceComparator.FromDistance(pos1 - pos2);
                Log("{0} and {1} have a separation of {2} spots ({3}).",
                    group1.NameAsSubject,
                    group2.NameAsSubject.ToLower(),
                    (pos1 - pos2),
                    result
                );

                return result;
            }

            protected int GetPosition(PersonCollection group)
            {
                Object[] groups = this.ToArray();
                PersonCollection curGroup;

                for (int i = groups.GetLowerBound(0); i <= groups.GetUpperBound(0); i++)
                {
                    curGroup = groups[i] as PersonCollection;
                    if (curGroup == group)
                        return i;
                }

                return -1;
            }

        }

        static private PersonCollection us, them;
        static private Person you, me;
        static private GroupQueue separation;


        /// <summary>
        ///        Initializes people and groups referred to in the song.
        /// </summary>
        static public void PopulateGroups()
        {
            me = new Person("Evan");

            us = new PersonCollection("We", "us");
            us.Add(me);
            us.Add(new Person("J.B."));
            us.Add(new Person("JoeDoc"));
            us.Add(new Person("Clio"));
            me.Friends = us;

            them = new PersonCollection("They", "them");
            them.Add(new Person("Shrub"));
            them.Add(new Person("Rummy"));
            them.Add(new Person("Cheney"));

            you = new Person("Karl Rove");
            you.Friends = them;

            separation = new GroupQueue();
            separation.Enqueue(us);

            string name;
            for (int i = 1; i < DistanceComparator.THRESH_FAR_AHEAD; i++)
            {
                name = "Separation Group #" + i;
                separation.Enqueue(new PersonCollection(name, name));
            }
            separation.Enqueue(them);
        }

        static protected void Log(string message)
        {
#if LOG_ENABLED
            System.Console.Error.WriteLine(">> " + message);
#endif
        }

        static protected void Log(string messageTemplate, params object[] parms)
        {
            Log(string.Format(messageTemplate, parms));
        }

        static protected void Output(string message)
        {
            System.Console.WriteLine(message);
        }

        static protected void Output(string messageTemplate, params object[] parms)
        {
            Output(string.Format(messageTemplate, parms));
        }



        /// <summary>
        ///     Entry point for console application.
        /// </summary>
        static public void Main()
        {
            Console.WriteLine("=================");
            Console.WriteLine("Men Without Hats");
            Console.WriteLine(" Safety Dance!");
            Console.WriteLine("----------------");
            Console.WriteLine();

            PopulateGroups();
            Intro();
            StanzaOne();

            Console.ReadLine();
        }


        /// <summary>
        ///        Processes the introduction of the song.
        /// </summary>
        static private void Intro()
        {
            const int REPEAT_COUNT = 4;

            StringBuilder sb = new StringBuilder();
            string ch;

            for (int iw = 0; iw < SAFETY_WORD.Length; iw++)
            {
                if (iw > 0)
                    sb.Append(" ");

                ch = SAFETY_WORD.Substring(iw, 1);
                for (int ir = 1; ir <= REPEAT_COUNT; ir++)
                {
                    sb.Append((ir > 1) ? ch : ch.ToUpper());
                    if (ir < REPEAT_COUNT)
                        sb.Append("-");
                }
            }

            Output(sb.ToString());
        }


        /// <summary>
        ///        Processes the first stanza of the song.
        /// </summary>
        static private void StanzaOne()
        {
            Output("We can dance if we want to");
            us.CanDance = true;

            Log("Can we leave them far behind: {0}", separation.RelativePosition(us, them) == RelativeLinearPosition.FarBehind);
            Output("We can leave your friends behind");

            Output("'Cause your friends don't dance...");
            them.CanDance = false;

            Output("...and if they don't dance");

            Output("Well they're no friends of mine");
            Log("Removing those friends of {0} who cannot dance", me.Name);
            foreach (Person person in them)
            {
                if (person.CanDance == false)
                {
                    if (me.Friends.Contains(person))
                    {
                        me.Friends.Remove(person);
                        Log("{0} is no longer a friend of {1}.",
                            person.Name,
                            me.Name
                        );
                    }
                    else
                    {
                        Log("{0} is not a friend of {1}; no need to remove.",
                            person.Name,
                            me.Name
                        );
                    }
                }
            }

            Output("I say, we can go where we want to");
            us.SetCanGo(Location.WhereWeWantTo, true);

            Output("A place where they will never find");
            if (them.CanFind(Location.WhereWeWantTo))
                throw new ApplicationException("They CAN find us!");
            Log("They cannot find us.");

            Output("And we can act like we come from out of this world");
            us.ActLikeWeComeFromOutOfThisWorld();

            Output("Leave the real one far behind.");
            us.LeaveTheRealWorldFarBehind();

            Output("And we can dance.");
            us.CanDance = true;
        }
    }
}
{% endcodeblock %}

Developed using Microsoft Visual C# Express Edition and builds cleanly.

Now **that** should more than settle the score.
