import yfinance as yf
import pandas as pd
import plotly.graph_objects as go

def calcular_rendimiento_acumulado(ticker, fecha_inicio):
    data = yf.download(ticker, start=fecha_inicio)
    data['Return'] = data['Close'].pct_change()
    data['Cumulative Return'] = (1 + data['Return']).cumprod()
    rendimiento_acumulado = (data['Cumulative Return'] - 1) * 100
    return rendimiento_acumulado

tickers = ['^GSPC', '^DJI', '^IXIC', 'GC=F', 'BTC-USD', 'ETH-USD']
fecha_inicio = '2023-01-01'
resultados = {}

for ticker in tickers:
    rendimiento = calcular_rendimiento_acumulado(ticker, fecha_inicio)
    resultados[ticker] = rendimiento

fig = go.Figure()

for ticker, rendimiento in resultados.items():
    fig.add_trace(go.Scatter(x=rendimiento.index, y=rendimiento, mode='lines', name=ticker))

fig.update_layout(
    title='Rendimiento Activos desde 2023-01-01',
    xaxis_title='Fecha',
    yaxis_title='Rendimiento (%)',
    legend_title='Activos',
)

fig.update_xaxes(
    mirror=True,
    ticks='outside',
    showline=True,
    linecolor='black',
    gridcolor='lightgrey'
)
fig.update_yaxes(
    mirror=True,
    ticks='outside',
    showline=True,
    linecolor='black',
    gridcolor='lightgrey'
)

fig.show()
