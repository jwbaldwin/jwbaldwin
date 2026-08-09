```elixir
defmodule WhoAmI do
  @enforce_keys [:location, :editor, :languages, :links]
  defstruct @enforce_keys

  def profile do
    %__MODULE__{
      location: "east coast",
      editor: :neovim,
      languages: ~w(elixir typescript go rust)a,
      links: [x: "https://x.com/jwbaldwin"]
    }
  end

  def spend(time) do
    with {:ok, time} <- tweak_neovim_config(time),
         task <- Task.async(fn -> build_things(time) end),
         {:ok, thing} <- Task.await(task) do
      thing
      |> ship()
      |> share()
    end
  end
end
```
