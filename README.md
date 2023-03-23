# myApp 
using System;
using System.Collections.Generic;

namespace MyApp
{
    // Classe Employee qui contient le nom de l'employé et sa liste de disponibilités
    class Employee
    {
        public string Name { get; set; }
        public List<Availability> Availabilities { get; set; }
    }

    // Classe Availability qui contient le jour de la semaine, l'heure de début et l'heure de fin de la disponibilité
    class Availability
    {
        public DayOfWeek DayOfWeek { get; set; }
        public TimeSpan StartTime { get; set; }
        public TimeSpan EndTime { get; set; }
    }

    class Program
    {
        // Liste qui contient tous les employés de l'entreprise
        static List<Employee> employees = new List<Employee>();

        static void Main(string[] args)
        {
            // Entrer les disponibilités d'un employé
            Employee employee1 = new Employee
            {
                Name = "John Doe",
                Availabilities = new List<Availability>
                {
                    new Availability
                    {
                        DayOfWeek = DayOfWeek.Monday,
                        StartTime = new TimeSpan(8, 0, 0),
                        EndTime = new TimeSpan(17, 0, 0)
                    },
                    new Availability
                    {
                        DayOfWeek = DayOfWeek.Tuesday,
                        StartTime = new TimeSpan(8, 0, 0),
                        EndTime = new TimeSpan(17, 0, 0)
                    },
                    new Availability
                    {
                        DayOfWeek = DayOfWeek.Wednesday,
                        StartTime = new TimeSpan(8, 0, 0),
                        EndTime = new TimeSpan(17, 0, 0)
                    },
                    new Availability
                    {
                        DayOfWeek = DayOfWeek.Thursday,
                        StartTime = new TimeSpan(8, 0, 0),
                        EndTime = new TimeSpan(17, 0, 0)
                    },
                    new Availability
                    {
                        DayOfWeek = DayOfWeek.Friday,
                        StartTime = new TimeSpan(8, 0, 0),
                        EndTime = new TimeSpan(17, 0, 0)
                    }
                }
            };
            // Ajouter l'employé à la liste des employés
            employees.Add(employee1);

            // Afficher les disponibilités d'un employé sélectionné
            Employee selectedEmployee = employees.Find(e => e.Name == "John Doe");
            foreach (Availability availability in selectedEmployee.Availabilities)
            {
                Console.WriteLine("Disponibilité : {0} de {1} à {2}", availability.DayOfWeek, availability.StartTime, availability.EndTime);
            }

            // Trouver les périodes de disponibilités pour les employés sélectionnés et la durée du rendez-vous sélectionnée
            DayOfWeek selectedDayOfWeek = DayOfWeek.Monday;
            TimeSpan selectedStartTime = new TimeSpan(10, 0, 0);
            TimeSpan selectedEndTime = new TimeSpan(11, 0, 0);

            // Filtrer les employés qui ont une disponibilité qui correspond aux critères sélectionnés
            List<Employee> selectedEmployees = employees.FindAll(e => e.Availabilities.Exists(a => a.DayOfWeek == selectedDayOfWeek && a.StartTime <= selectedStartTime && a.EndTime >= selectedEndTime));

            // Ajouter toutes les heures disponibles des employés sélectionnés dans une liste
            List<TimeSpan> availableTimes = new List<TimeSpan>();
            foreach (Employee selectedEmployee in selectedEmployees)
            {
                foreach (Availability availability in selectedEmployee.Availabilities)
                {
