    <Window x:Class="WpfAppGrafika3Psroda.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:WpfAppGrafika3Psroda"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <Grid>
        <TabControl>
            <TabItem Header="Przyciski karuzela">
                <UniformGrid Rows="1">
                    <Button Margin="30" Click="Button_Click">Nazot</Button>
                    <Image Source="grafika/rys1.jpg"
               x:Name="obraz"/>
                    <Button Margin="30" Click="Button_Click_1">Dalej</Button>
                </UniformGrid>
            </TabItem>
            <TabItem Header="Radio">
                <StackPanel Orientation="Horizontal">
                    <StackPanel>
                        <RadioButton 
                            GroupName="obrazki_radio"
                            x:Name="rys1"
                            Checked="rys1_Checked">
                            Zdjęcie 1
                        </RadioButton>
                        <RadioButton 
                            GroupName="obrazki_radio"
                            x:Name="rys2">
                            Zdjęcie 2
                        </RadioButton>
                        <RadioButton 
                            GroupName="obrazki_radio"
                            x:Name="rys3">
                            Zdjęcie 3
                        </RadioButton>
                    </StackPanel>
                    <Image 
                        Source="../../../grafika/rys4.jpg"
                        x:Name="obrazek2"/>
                </StackPanel>
            </TabItem>
            <TabItem Header="combobox">
                <StackPanel>
                      <ComboBox x:Name="combo_box" 
                              SelectionChanged="combo_box_SelectionChanged" >
                        <ComboBoxItem>1</ComboBoxItem>
                        <ComboBoxItem>2</ComboBoxItem>
                        <ComboBoxItem>3</ComboBoxItem>
                        <ComboBoxItem>4</ComboBoxItem>
                    </ComboBox>
                    <Image
                        x:Name="obrazek3"
                        Source="grafika/rys8.jpg"/>
                </StackPanel>
            </TabItem>
        </TabControl>
    </Grid>
    </Window>





    ﻿using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows;
    using System.Windows.Controls;
    using System.Windows.Data;
    using System.Windows.Documents;
    using System.Windows.Input;
    using System.Windows.Media;
    using System.Windows.Media.Imaging;
    using System.Windows.Navigation;
    using System.Windows.Shapes;

    namespace WpfAppGrafika3Psroda
    {
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public List<BitmapImage> Images { get; set; }
        public int Aktualny { get; set; }
        public MainWindow()
        {
            InitializeComponent();
            przygotujObrazy();
            Aktualny = 0;
        }

        private void przygotujObrazy()
        {
            Images= new List<BitmapImage>();
            Images.Add(new BitmapImage(new Uri("grafika/rys1.jpg", UriKind.Relative)));
            Images.Add(new BitmapImage(new Uri("grafika/rys2.jpg", UriKind.Relative)));
            Images.Add(new BitmapImage(new Uri("grafika/rys3.jpg", UriKind.Relative)));
            Images.Add(new BitmapImage(new Uri("grafika/rys4.jpg", UriKind.Relative)));
            Images.Add(new BitmapImage(new Uri("grafika/rys5.jpg", UriKind.Relative)));
            Images.Add(new BitmapImage(new Uri("grafika/rys6.jpg", UriKind.Relative)));
            Images.Add(new BitmapImage(new Uri("grafika/rys7.jpg", UriKind.Relative)));
            Images.Add(new BitmapImage(new Uri("grafika/rys8.jpg", UriKind.Relative)));
        }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
            Aktualny--;
            if (Aktualny < 0)
            {
                Aktualny = Images.Count - 1;
            }
            obraz.Source = Images[Aktualny];

        }

        private void Button_Click_1(object sender, RoutedEventArgs e)
        {
            Aktualny++;
            if (Aktualny == Images.Count)
                Aktualny = 0;
            obraz.Source = Images[Aktualny];
        }

        private void rys1_Checked(object sender, RoutedEventArgs e)
        {
            obrazek2.Source = new BitmapImage(new Uri("grafika/rys1.jpg",UriKind.Relative));
        }

        private void combo_box_SelectionChanged(object sender, SelectionChangedEventArgs e)
        {
            int ktory = combo_box.SelectedIndex;
            obrazek3.Source = Images[ktory];
        }
    }
    }
