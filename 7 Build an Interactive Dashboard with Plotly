# Import required libraries
import pandas as pd
import dash
import dash_html_components as html
import dash_core_components as dcc
from dash.dependencies import Input, Output
import plotly.express as px

# Read the airline data into pandas dataframe
spacex_df = pd.read_csv("spacex_launch_dash.csv")
max_payload = spacex_df['Payload Mass (kg)'].max()
min_payload = spacex_df['Payload Mass (kg)'].min()

# Create a dash application
app = dash.Dash(__name__)

# Create an app layout
app.layout = html.Div(children=[html.H1('SpaceX Launch Records Dashboard',
                                        style={'textAlign': 'center', 'color': '#503D36',
                                               'font-size': 40}),
                                # TASK 1: Add a dropdown list to enable Launch Site selection
                                # The default select value is for ALL sites
                                dcc.Dropdown(
                                id='site-dropdown',
                                    options=[
                                        {'label':'ALL SITES','value':'ALL'},
                                        {'label':'CCAFS LC-40','value':'site1'},
                                        {'label':'CCAFS SLC-40','value':'site2'},
                                        {'label':'KSC LC-39A','value':'site3'},
                                        {'label':'VAFB SLC-4E','value':'site4'},
                                    ],
                                    value='ALL',
                                    placeholder='Select a launch site',
                                    searchable=True
                                    ),
                                html.Br(),
])

                                # TASK 2: Add a pie chart to show the total successful launches count for all sites
                                # If a specific launch site was selected, show the Success vs. Failed counts for the site
html.Div(dcc.Graph(id='success-pie-chart')),
html.Br(),
                                # Function decorator to specify function input and output
@app.callback(
    Output(component_id='success-pie-chart', component_property='figure'),
    Input(component_id='site-dropdown', component_property='value'))
def get_pie_chart(entered_site):
    filtered_df = spacex_df
    if entered_site == 'ALL':
        fig = px.pie(data, values='class', 
        names='pie chart names', 
        title='title')
        return fig
    else:
        entered_site=='site1'
        site1_=spacex_df.groupby('class')['class'].count().reset_index()
        s_chart1=dcc.Graph(
            fig=px.get_pie_chart(site1_,
            names='Failed','Success',
            title='Total CCAFS LC-40 Launches'))
            
        entered_site=='site2'
        site2_=spacex_df.groupby('class')['class'].count().reset_index()
        s_chart2=dcc.Graph(
            fig=px.get_pie_chart(site2_,
            names='Failed','Success',
            title='Total CCAFS SLC-40 Launches'))

        entered_site=='site3'
        site3_=spacex_df.groupby('class')['class'].count().reset_index()
        s_chart3=dcc.Graph(
            fig=px.get_pie_chart(site3_,
            names='Failed','Success',
            title='Total KSC LC-39A Launches'))

        entered_site=='site4'
        site4_=spacex_df.groupby('class')['class'].count().reset_index()
        s_chart4=dcc.Graph(
            fig=px.get_pie_chart(site4_,
            names='Failed','Success',
            title='Total VAFB SLC-4E Launches'))

        return [
            html.Div(className='chart item',style={'display':'flex'})
        ]

                            html.P("Payload range (Kg):"),
                                # TASK 3: Add a slider to select payload range
                                dcc.RangeSlider(
                                    id='payload-slider',
                                    min=0, 
                                    max=10000, 
                                    step=1000,
                                    marks={0: '0',
                                            100: '100'},
                                    value=[min_value, max_value])

                                # TASK 4: Add a scatter chart to show the correlation between payload and launch success
                                html.Div(dcc.Graph(id='success-payload-scatter-chart')),
                                

# TASK 2:
# Add a callback function for `site-dropdown` as input, `success-pie-chart` as output

# TASK 4:
# Add a callback function for `site-dropdown` and `payload-slider` as inputs, `success-payload-scatter-chart` as output
# Function decorator to specify function input and output
@app.callback(Output(component_id='success-payload-scatter-chart', component_property='figure'),
              [Input(component_id='site-dropdown', component_property='value')Input(component_id='payload-slider',component_property='value')])
def get_scatter_chart(entered_site):
    filtered_df = spacex_df
    if entered_site == 'ALL':
        fig = px.scatter(data, values='Payload Mass', 
        color='BoosterVersion Category',
        x='Payload Mass',
        y='class', 
        title='title')
        return fig
    else:
        entered_site=='site1'
        site_1_=spacex_df.groupby('class')['Payload Mass'].sum().reset_index()
        PLM_chart1=dcc.Graph(
            fig=px.get_scatter_chart(site_1_,
            x='Payload Mass (kg)',
            y='Launch Classification',
            color='Booster Version Category',
            title='CCAFS LC-40 Launch Outcomes with Payload Mass'))

        entered_site=='site2'
        site_2_=spacex_df.groupby('class')['Payload Mass'].sum().reset_index()
        PLM_chart2=dcc.Graph(
            fig=px.get_scatter_chart(site_2_,
            x='Payload Mass (kg)',
            y='Launch Classification',
            color='Booster Version Category'
            title='CCAFS SLC-40 Launch Outcomes with Payload Mass'))

        entered_site=='site3'
        site_3_=spacex_df.groupby('class')['Payload Mass'].sum().reset_index()
        PLM_chart3=dcc.Graph(
            fig=px.get_scatter_chart(site3_,
            x='Payload Mass (kg)',
            y='Launch Classification',
            color='Booster Version Category',
            title='KSC LC-39A Launch Outcomes with Payload Mass'))

        entered_site=='site4'
        site_4_=spacex_df.groupby('class')['Payload Mass'].sum().reset_index()
        PLM_chart4=dcc.Graph(
            fig=px.get_scatter_chart(site_4_,
            x='Payload Mass (kg)',
            y='Launch Classification',
            color='Booster Version Category'
            names='Failed','Success',
            title='VAFB SLC-4E Launch Outcomes with Payload Mass'))
return [
            html.Div(className='chart item',style={'display':'flex'})
        ]

# Run the app
if __name__ == '__main__':
    app.run_server(debug=True)
